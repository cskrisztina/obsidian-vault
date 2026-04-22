


  

https://www.coursera.org/learn/python-for-applied-data-science-ai/lecture/qmo2G/introduction-to-python

 Jupyter: egy **interaktív fejlesztői környezet**, amit a böngészőben használsz.

  
### **1. Logolás (naplózás)**

Pythonban a `**logging**` modult használjuk a program eseményeinek nyomon követésére. Példa:

import logging# Alap beállítás: kiírja a log üzeneteket a konzolra:
logging.basicConfig(level=logging.INFO)x = 5y = 0logging.info(f"x értéke: {x}")

- logging.info`()` – normál információk
    
- `logging.warning()` – figyelmeztetések
    
- `logging.error()` – hibák
    

Ez hasznos, mert **nyomon követheted, mi történik a kód futása közben**.

---

### **2. Hibakeresés (debugging)**

A legegyszerűbb mód a `**print()**` vagy a Python beépített `**breakpoint()**` használata:

x = 5y = 0# Debug: itt a futás megáll, beléphetsz interaktívanbreakpoint() z = x / y # itt hiba lesz, de a breakpoint előtt ellenőrizheted x, y értékét

- A `**breakpoint()**` a kód futását megszakítja, és beléphetsz egy interaktív konzolba, ahol ellenőrizheted a változókat.
    
- Ha Jupyter-ben vagy, egyszerűen használhatod a `**print()**`-et a hibakereséshez:
    

print(f"x={x}, y={y}")

  

  
Típusok: **Python alapvető típusai**:

- **Számok**:
    

- `int` – egész számok (pl. `5`)
    
- `float` – lebegőpontos számok (pl. `3.14`)
    
- `complex` – komplex számok (pl. `2 + 3j`)
    

- **Szöveg**:
    

- `str` – karakterláncok (pl. `"Hello"`)
    

- **Logikai érték**:
    

- `bool` – `True` vagy `False`
    

- **Lista és gyűjtemények**:
    

- `list` – rendezett, módosítható lista (pl. `[1,2,3]`)
    
- `tuple` – rendezett, nem módosítható (pl. `(1,2,3)`)
    
- `set` – halmaz, egyedi elemek (pl. `{1,2,3}`)
    
- `dict` – kulcs-érték párok (pl. `{"név":"Anna","kor":25}`)