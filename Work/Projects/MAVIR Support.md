
**Liferay verzió**: Liferay DXP 7.4.13 Update 65 (Cavanaugh / Build 7413 / February 24, 2023)

 - proj.környezet: [https://mavir-74.dev.webtown.cloud/web/intranet](https://mavir-74.dev.webtown.cloud/web/intranet)
 - belépés:[admin@test.com](mailto:admin@test.com) / admin 
 - gitlab:[https://gitlab.ci.webtown.cloud/webtownhu/mavir-7.4](https://gitlab.ci.webtown.cloud/webtownhu/mavir-7.4)


# MAVIR Oracle Dump – Lokális környezet felállítása

> **Fontos:** Olvasd végig az egész dokumentumot mielőtt nekilátsz!

---

## Előfeltételek

- Docker telepítve van
- Oracle dump fájlok elérhetők lokálisan (`intrat_exp_20260415_*.dmp`)
- Liferay workspace repo klónozva (ojdbc10.jar miatt)

---

## 1. lépés – Oracle Docker konténer indítása

```bash
docker run -d --name oracle-free \
  -p 1521:1521 \
  -e ORACLE_PASSWORD=oracle \
  gvenzl/oracle-free
```

**Megjegyzések:**
- Oracle **23**-as verziót használj – a 21-es túl régi a dumphoz és nem fog működni
- Az adatbázis az `1521`-es porton lesz elérhető
- Jelszó: `oracle`
- Service name: `FREEPDB1`

### Ellenőrzés – várj amíg elindul:

```bash
docker logs -f oracle-free
```

✅ Ha megjelenik a `DATABASE IS READY TO USE` sor, mehet a következő lépés.

---

## 2. lépés – Dump fájlok bemásolása a konténerbe

Navigálj abba a könyvtárba ahol a `.dmp` fájlok vannak, majd:

```bash
docker cp . oracle-free:/tmp/
```

---

## 3. lépés – Oracle séma létrehozása

Lépj be a konténerbe:

```bash
docker exec -it oracle-free bash
```

Csatlakozz `sqlplus`-szal:

```bash
sqlplus system/oracle@FREEPDB1
```

Hozd létre az `INTRAT` usert és állítsd be a `dp_dir` könyvtárat:

```sql
CREATE USER INTRAT IDENTIFIED BY oracle;
GRANT CONNECT, RESOURCE TO INTRAT;
GRANT UNLIMITED TABLESPACE TO INTRAT;

CREATE OR REPLACE DIRECTORY dp_dir AS '/tmp';

EXIT;
```

---

## 4. lépés – Dump importálása

Még mindig a konténeren belül, futtasd az `impdp`-t:

```bash
impdp system/oracle@FREEPDB1 \
  DIRECTORY=dp_dir \
  DUMPFILE=intrat_exp_20260415_%U.dmp \
  LOGFILE=import.log \
  TABLES=INTRAT.% \
  REMAP_TABLESPACE=DATA:USERS
```

**Paraméterek magyarázata:**
| Paraméter | Leírás |
|---|---|
| `DIRECTORY=dp_dir` | A `/tmp` mappára mutat ahol a dumpok vannak |
| `DUMPFILE=..._%U.dmp` | `%U` – az összes számozott dump fájlt beimportálja |
| `TABLES=INTRAT.%` | Csak a táblákat importálja (nem permissionöket stb.) |
| `REMAP_TABLESPACE=DATA:USERS` | Az ő `DATA` tablespace-ük helyett a `USERS`-t használja |

> Ha az import után az `INTRAT` user jelszava nem `oracle` lenne, állítsd vissza:
> ```sql
> sqlplus system/oracle@FREEPDB1
> ALTER USER INTRAT IDENTIFIED BY oracle;
> EXIT;
> ```

---

## 5. lépés – ⚠️ ComponentBlacklist törlése (PORTÁL INDÍTÁSA ELŐTT!)

**Ezt kötelező megcsinálni mielőtt először elindítod a Liferay portált!**

Ha az import után először indítod el a portált a törlés nélkül, a blacklist becacheli magát és semmi nem fog elindulni – újra kell húzni az egészet.

Nyisd meg az adatbázist (pl. DBeaver vagy sqlplus), és töröld a `Configuration` táblából a `ComponentBlacklist` bejegyzést:

```sql
-- Kapcsolódj INTRAT userrel vagy system userrel
DELETE FROM INTRAT.CONFIGURATION WHERE ... -- keresd meg a ComponentBlacklist sort és töröld
COMMIT;
```

---

## 6. lépés – Liferay portal-ext.properties beállítása

Add hozzá a `portal-ext.properties` fájlhoz az Oracle kapcsolódási adatokat:

```properties
jdbc.default.driverClassName=oracle.jdbc.OracleDriver
jdbc.default.url=jdbc:oracle:thin:@//localhost:1521/FREEPDB1
jdbc.default.username=INTRAT
jdbc.default.password=oracle
```

---

## 7. lépés – ojdbc10.jar elhelyezése

Másold be az `ojdbc10.jar` fájlt ide:

```
tomcat-<verzió>/webapps/ROOT/WEB-INF/shielded-container-lib/
```

A jar megtalálható a workspace repóban is.

---

## 8. lépés – Liferay indítása és modulok telepítése

- Java **11**-gyel fordíts és futtass (a kód Java 8-ra lő, de 11-gyel működik)
- Telepítsd ki **az összes** intranetes modult – különben el lesz törve itt-ott a portál

---

## Referencia linkek

- **Dev környezet:** https://mavir-74.dev.webtown.cloud/web/intranet (admin@test.com / admin)
- **GitLab repo:** https://gitlab.ci.webtown.cloud/webtownhu/mavir-7.4

---

## Gyors összefoglaló – parancsok sorban

```bash
# 1. Konténer indítás
docker run -d --name oracle-free -p 1521:1521 -e ORACLE_PASSWORD=oracle gvenzl/oracle-free

# 2. Dump fájlok másolása (dump könyvtárból futtatva)
docker cp . oracle-free:/tmp/

# 3. Belépés + séma létrehozás
docker exec -it oracle-free bash
sqlplus system/oracle@FREEPDB1
# → SQL parancsok: CREATE USER, GRANT-ok, CREATE DIRECTORY

# 4. Import
impdp system/oracle@FREEPDB1 DIRECTORY=dp_dir DUMPFILE=intrat_exp_20260415_%U.dmp LOGFILE=import.log TABLES=INTRAT.% REMAP_TABLESPACE=DATA:USERS

# 5. ComponentBlacklist törlése DB-ből

# 6-7. portal-ext.properties + ojdbc10.jar beállítás

# 8. Liferay indítás + modulok telepítése
```