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
- Hotovo: úvodní průvodce (úložiště telefon/Google Disk, šifrování heslem AES-GCM, údaje, vybavení, kotouče, maxima, střídání míst), profil, posilovna 4 dny po ~55–60 min, vlastní váha 2 kruhové tréninky + kardio + kliky po troškách, režim podle kalendáře, odlehčení po návratu do posilovny, sloty se 3 náhradami (swipe/šipky), kalibrace z maxim a ze sérií, adaptivní tempo, diagnóza poklesu, přenos vynechaných partií, rozcvička, zápis starších tréninků, kalendář, váha, záloha do souboru.
- Kód: vše v `index.html` (katalog `X(...)`, programy `PROGRAM` se sloty `S(...)`, figury `PAT`, výpočty, sync, obrazovky).
- Hotovo také: přehled Dnes, Jídlo (vestavěné potraviny `FOODS`, vlastní potraviny, rychlé znovu, porce, cíle kcal/makra z profilu s úpravou podle trendu váhy, voda, kreatin, kofein, návrh jídelníčku `PLANS`, čárový kód přes BarcodeDetector + Open Food Facts, foto obalu přes Tesseract.js), Peníze (ruční výdaje, ceny z jídla, kategorie `MCATS`, rozpočet, kurz €, 6 měsíců, top položky, import CSV výpisu z banky).
- Další nápady: přímé napojení banky (Fio API), úpravy záznamů, export, foto jídla s AI.
