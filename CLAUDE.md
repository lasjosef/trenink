# Trénink – osobní appka

Offline PWA: trénink, později jídlo a peníze. Každý uživatel si při prvním spuštění vybere úložiště (jen telefon / vlastní Google Disk) a vyplní své údaje.
Běží na GitHub Pages: https://lasjosef.github.io/trenink (Android, Chrome, „Přidat na plochu“).

## Pravidla
- UI je česky.
- Funguje offline (posilovna bez internetu). `sw.js` = cache; při každé změně appky zvyš verzi `V` v `sw.js`.
- Žádný server. Data jsou v `localStorage` telefonu a záloha na jeho Google Disk (scope `drive.file`, vlastní složka „Trénink“ na Disku přihlášeného uživatele). `CLIENT_ID` v `index.html` z Google Cloud (origin `https://lasjosef.github.io`).
- Žádná osobní data do repozitáře (je veřejný). Údaje o uživateli patří jen do úvodního nastavení v appce.
- Pop-upy/modaly ne, preferuj inline panely.

## Stav (listopad 2026)
- Hotovo: posilovna Horní/Spodní 4× týdně (rotace H1→S1→H2→S2), kalibrace síly z sérií (3+ / 1–2 / Hranice = RIR 3 / 1,5 / 0,5), adaptivní tempo růstu, diagnóza poklesu, check-in jen do rozboru, lehčí den −5 %, odškrtávání sérií, čas od „Jdu na to“, přenos vynechaných cviků podle partií, rozcvička u těžkých cviků, zápis starších tréninků, kalendář, tělesná váha, synchronizace na Disk.
- Plán: horní/spodní den na 60 min, ≥3 náhrady cviku (swipe), program s vlastní vahou (doma / na cestách), rotace posilovna ↔ vlastní váha podle kalendáře, úvodní nastavení s volbou úložiště, šifrování dat heslem před nahráním na Disk, jídlo (oblíbené, čárový kód přes Open Food Facts, foto tabulky obalu s OCR v telefonu, kreatin/protein), peníze (výdaje, kategorie, banka).
- Kotouče v nastavení (výchozí 25/20/15/10/5/2,5 kg).
