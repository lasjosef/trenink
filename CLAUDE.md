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
- Hotovo také: přehled Dnes, Jídlo (vestavěné potraviny `FOODS`, vlastní potraviny, rychlé znovu, porce, cíle kcal/makra z profilu s úpravou podle trendu váhy, voda, kreatin, kofein, návrh jídelníčku `PLANS`, čárový kód přes BarcodeDetector + Open Food Facts, foto obalu přes Tesseract.js `OCR_LANGS` CZ/SK/PL/DE/EN; když OFF nemá hodnoty, hned nabídne foto tabulky; Dnes → „Rychle zapsat“ `qa*`: našeptávač z vlastních potravin + OFF search.pl s obrázky, kód, foto, počet kusů a cena → deník i výdaje, Vrátit), Peníze (ruční výdaje, ceny z jídla, kategorie `MCATS`, rozpočet, kurz €, 6 měsíců, top položky, import CSV výpisu z banky).
- Vzhled: barvy sekcí podle kotoučů (Dnes modrá, Trénink červená, Jídlo zelená, Peníze žlutá), světlý i tmavý režim, spodní lišta s ikonami, swipe mezi záložkami (`TABS`), kalorie jako kotoučový kruh (`plateRing`). Jídlo: přehled po jídlech dne s +, přidávání na vlastní obrazovce (`fAdd`). Doplňky v Profilu (`PROFILE.doplnky`, dávka, kolikrát denně, propojení s potravinou).
- Jídelníček: `MEALLIB` (jídla po slotech s recepty a štítky), `PRICE` (Kč/kg, v DE přepočet na €), `solvePlan` hledá kombinaci + společné měřítko porcí na kcal/bílkoviny/rozpočet, varianty swipem (`replanDay`), zápis do deníku. Nákup: seznam z plánu na 1/3/7 dní, obchody v okolí přes Overpass (OSM) + Nominatim, verdikt „Koupit, nebo ne?“ z Open Food Facts. Rady „čeho víc a čeho míň“ (`insightsHTML`). Rozpočet na jídlo den/týden v Profilu.
- Kuchyně: nádobí v Profilu (`KIT`, `PROFILE.kuchyne`), recepty z ruky (`HAND_REQ`) + generované (`GEN` = bílkovina × příloha × dochucení, kroky `genSteps` podle nádobí), výběr `eligible`/`sampleOpts`. Jídlo → Vaření: hledání víc slov najednou (`matchQuery`, název+suroviny+nádobí), filtry podle nádobí (`eqOf`), recept s porcemi, cenou, obchody; postup `genSteps(r,K,n)` s přesnými gramy, lžícemi, várkami do airfryeru, minutkami; vaření do zásoby a mrazák (záznam `mrazak`), plán mrazák upřednostňuje.
- Foto jídla s AI: fotka v IndexedDB (`photoPut`), záznam `fid:"foto"` s náhledem `thumb` a `pending`; `aiProcessPending` po startu/online pošle fotku + název do Gemini (`gemini-flash-latest`) nebo Claude API, klíč jen v `localStorage` `tr4_ai` (nesynchronizuje se). Ruční jídla mají podrobné kroky (`HAND_MAP` přes stavebnice, `HAND_STEPS`), vše přes `recipeSteps`. Do Vaření nepatří bistro/obchod (`isRecipe`).
- Další nápady: přímé napojení banky (Fio API), export.
