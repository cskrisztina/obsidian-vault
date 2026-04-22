  

proj.környezetünkre basic auth:

username:sda-7-4

pw:webtown2024

  

  

VPN:

Krisztina Csombor

  

kcsombor

P>O(AYC[7cgx$bBy?%

[kcsombor@SDA.GOV.SA](mailto:kcsombor@SDA.GOV.SA)

  

  

SDA hozzáférések

# GIT

[https://gitlab.ci.webtown.hu/webtown/sda-7.4](https://gitlab.ci.webtown.hu/webtown/sda-7.4)

p_admin/p_admin

  

# Jenkins

[https://jenkins.ci.webtown.hu/job/sda-7.4/](https://jenkins.ci.webtown.hu/job/sda-7.4/)

# Környezetek

## WT Cloud

[https://sda-7-4.dev.webtown.cloud/](https://sda-7-4.dev.webtown.cloud/)

[test@sda.gov.sa](mailto:test@sda.gov.sa) / test2

  

  

SDA sda dev:[http://10.10.14.51:8080/](http://10.10.14.51:8080/)

  

local: test@sda.gov.sa

test2

  
  

fragment :

zippelni az egész mappát és kézzel kitenni

  

sda-node:local indítása:

  

- npm install (ez telepíti a node.js és a crafton kódhoz tartozó dependencyket is)
    
- npm run build (ez lebuildeli a craftonos kódot, kijavítja a fontok és képek útvonalát, és berakja a megfelelő helyre a main.css és main.js fájlokat (valamint a hozzájuk tartozó source mapet is))
    
- npm run start-local (localhost módban elindítja az appot, mind eddig is, csak raktam bele egy kötőjelet, hogy ne kelljen idézőjel)
    

  

  

  

**SDA INTRANET**

  

fragmenteknél:

`npm run build`

aztán

```
npm run compress
```


aztán buildben lévő zipet átmásolni a deployba

cd build && cp liferay-fragments.zip /home/csombork/Develop/Liferay/bundles/sda-7.4-u86/deploy

Crafton kód modosítsához **:html** mappában npm install aztán  npm run development

liferayes package.json be átírni: "themes\\sda-theme"

Webtown + sda vpn:

1.

sudo apt install openfortivpn

2.

sudo gedit (vagy amivel akarod szerkeszteni, nano, vi stb) /etc/openfortivpn/config

host = [93.112.39.178](http://93.112.39.178)

port = 10443

username = <username>

password = <password>

sudo openfortivpn

Elfog szállni, viszont a hiba üzenetben ott lesz, hogy kell a cert és ott lesz egy olyan sor hogy:

trusted-cert = ...

Ezt a sort az előbbi konfigba még adjuk hozzá

4.   
    

  

sudo openfortivpn

  

Elkezd belépni, és kérni fogja a két faktoros token-t (mobil) és belép

host = 93.112.39.178

port = 10443

username = kcsombor

password = SF{9&a.dRDm%xTf~

trusted-cert = f6a2e2ba15ca9fd83cf7166f163068224aed8f5d99f5468d703102f22581a69e

---

magic login link SDA UAT-on loginra [https://portal-uat.sda.gov.sa/home?p_p_id=com_liferay_login_web_portlet_LoginPortlet&p_[…]t_mvcRenderCommandName=%2Flogin%2Flogin&saveLastPath=false](https://portal-uat.sda.gov.sa/home?p_p_id=com_liferay_login_web_portlet_LoginPortlet&p_p_lifecycle=0&p_p_state=maximized&p_p_mode=view&_com_liferay_login_web_portlet_LoginPortlet_mvcRenderCommandName=%2Flogin%2Flogin&saveLastPath=false)

  

p_admin

test

  

  

Szükség lehet log nézésre, annak ez lenne a menete:

- [https://pam01.sda.gov/](https://pam01.sda.gov/)
    
    SAML authttal kell belépni
    
- local accounts tabon-load all account->access
    
- request tabon kiválasztani liferayes -xview request detailed->start session->manual_Ykimásolni az ssh elérést
    
- pamon keresztül eljuttok egy DEV-es SSH sessionig. Onnak meg a terminálból ssh-zva át tudtok ugrani uat-re így: ssh [bzsolt@10.10.16.51](mailto:bzsolt@10.10.16.51)
    
    pw:bzsolt@2030
    
- (52es végű a másik láb)
    
- jelszót fog kérni, ezt Ervinnek elküldtem
    
- itt meg ugyanaz minden, a Liferay-t is ugyanazon az útvonalon találjátok, mint ahogy a devnél van leírva az SDA - DEV környezet doksiban. Serveruserrel tudtok majd logot nézni, ha kellene.
    
- sudo su - serveruser
    
- liferay home: /opt/liferay-dxp
    
- uat környezet meg itt van: [http://10.10.16.51:8080/](http://10.10.16.51:8080/)
    

  

  

DEV-es log nézegetés: sudo su - serveruser

PW:View részleteiben (View Request Details) > Retrieve Password - Password (ssh user pass)

  

[https://docs.google.com/document/d/1Isy3NuACqP5GrlA7R9IBXWErBn9qSSr003Al-DfX5FI/edit#heading=h.pi9u6toukzh9](https://docs.google.com/document/d/1Isy3NuACqP5GrlA7R9IBXWErBn9qSSr003Al-DfX5FI/edit#heading=h.pi9u6toukzh9)

  

példa curl hívásra:

curl -H "Authorization:Bearer uYHiyPCus6WF1zeBQ2zB1XHVFQ078ms1qu3yPcuCfCT1IOAldCDOezKoH8oKQGmsAflTdFBJzuhwpIpXvoQysAQ3do>" https://api.sda.gov.sa/courses/balolayan@sda.gov.sa

  

  

  

curl -H "Authorization:Bearer uYHiyPCus6WF1zeBQ2zB1XHVFQ078ms1qu3yPcuCfCT1IOAldCDOezKoH8oKQGmsAflTdFBJzuhwpIpXvoQysAQ3do>" [http://10.10.14.67:8080/requests/balolayan@sda.gov.sa](http://10.10.14.67:8080/requests/balolayan@sda.gov.sa)

  

  

  

## DEV liferay

[http://10.10.14.51:8080/](http://10.10.14.51:8080/)

p_admin / test

Site: SDA Website