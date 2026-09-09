# Alapbeállítások, vásárlási folyamat, fizetés/szállítás, nyelvek, jog/GDPR

**Főmenü:** `Beállítások`

## Alapbeállítások
**Hivatalos:** https://unas.hu/tudastar/admin/alapbeallitasok
**Menü:** `Beállítások / Alapbeállítások` — lapfülekkel: Kategória, Termék,
Vásárló, **Megrendelés**, **Működés**, **Megjelenés**, Marketing.
- Kereső a lapon belül (beírt szóra szűri a beállításokat).
- **Működés** lapfül: itt kapcsolható a **szerverre mentett kosár** (elhagyott
  kosár / kosárra szóló követő hírlevél előfeltétele), szűrés-box beállítások.
- **Megrendelés** lapfül: mit keressen a rendelés-kereső; mi jelenjen meg a
  rendelés-értesítő e-mailben (pl. „a fizetési és szállítási módhoz tartozó
  részletes leírás"); fizetési/szállítási mód választási sorrend.
- **Megjelenés** lapfül: pl. raktárkészlet mutatása a vásárlói felületen.

## Vásárlási folyamat
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlasi-folyamat
**Menü:** `Beállítások / Vásárlási folyamat` — almenük: megrendelés
státuszok/típusok, megrendelés paraméterek, vásárló paraméterek, értesítések
(`references/ertesitesek-cseremezok.md`), visszáru, e-mail-ellenőrzés,
cím-ellenőrzés, gyorsrendelés, megrendelés törlés.
- **Hírlevél-feliratkozó jelölőnégyzet a pénztárban** itt / az Alapbeállításokban
  kapcsolható be. **Alapból ne legyen bepipálva** (előre bepipált = jogsértő).

## Fizetési módok
**Hivatalos:** https://unas.hu/tudastar/admin/fizetesi-modok
**Menü:** `Beállítások / Fizetés, Szállítás, Logisztika / Fizetési módok`
- Alap: Készpénzzel a helyszínen / Előre utalással / Utánvéttel. `Hozzáad` újhoz.
- Mezők: `Azonosító a Webáruházban` (export/importhoz), megnevezés, leírás,
  **alternatív leírás** (az értesítő e-mailekben ez jelenik meg, ha ki van
  töltve), típus (átutalás / készpénz / utánvét / csekk / egyéb), kezelési
  költség, aktív.
- Online kártya / részletfizetés: `Bankkártyás, speciális fizetési módok`
  almenü (Barion, SimplePay, OTP, PayPal, áruhitel stb.).

## Szállítási módok
**Hivatalos:** https://unas.hu/tudastar/admin/szallitasi-modok
- `Hozzáad`; `Azonosító a Webáruházban`, megnevezés, leírás, alternatív leírás
  (értesítőben), nyelvenkénti szövegek, aktív kapcsoló, szállítási költség.
- **Speciális szállítási módok** almenü: futár API-k / fájl integrációk
  (`references/megrendelesek.md` — csomagfeladás).
- Kapcsolódó: szállítási költségek, szállítási területek, átvételi pontok,
  országok kezelése, kiszervezett logisztika (3PL/fulfilment).

## Szállítás és fizetés kapcsolás
**Hivatalos:** https://unas.hu/tudastar/admin/szallitas-es-fizetes-kapcsolas
- Fizetési módonként korlátozható, mely szállítási mód választható (pl.
  „Készpénz a helyszínen" → csak „Személyes átvétel"). Fizetési módonként min. 1
  szállítási mód kell.

## Pénznemek, árkijelzés
**Hivatalos:** https://unas.hu/tudastar/admin/penznemek-arkijelzes
- Több pénznem, ÁFA-beállítások, árformátum (kerekítés, kijelzés).

## Nyelvek beállítása
**Hivatalos:** https://unas.hu/tudastar/admin/nyelvek-beallitasa
**Menü:** `Beállítások / Szövegek, Nyelvek / Nyelvek beállítása`
- Alapnyelv + további nyelvek; nyelvenként pénznem. Hiányzó fordítások:
  `Beállítások / Szövegek, Nyelvek / Alapszövegek`. Nyelvenként külön domain
  kérhető (ügyfélszolgálat). Nyelv **törlése törli** a hozzá tartozó szövegeket.
- Külön ország több adminnal = külön Unas webáruház, nem nyelv.

## Jog / GDPR
**Vásárlási feltételek:** https://unas.hu/tudastar/admin/vasarlasi-feltetelek
- Kötelező dokumentumok: ÁSZF, Adatkezelési tájékoztató, Elállási nyilatkozat.
  Két integrált ÁSZF-szolgáltató — tőlük rendelve a dokumentumok automatikusan
  frissülnek.
- **Adatkezelési beállítások:** https://unas.hu/tudastar/admin/adatkezelesi-beallitasok
  Cookie-k: működési vs. marketing. Cookie-sáv 3 típus (egyszerű nyugtázó /
  „Engedélyezem–Nem" / checkbox+mentés). Marketing cookie csak hozzájárulás
  után aktív (kivéve, ha az üzemeltető személyes azonosításra alkalmatlannak
  ítéli). Profilalkotás beállítás.
- **Privacy-first alap:** cookie-sávnál a nem-esszenciálisokat alapból ne
  engedélyezd.
