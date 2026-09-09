# Megrendelések: lista, részletek, státuszok, csomagfeladás, visszáru, számlázás, összeszedés, export

**Főmenü:** `Megrendelések`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/megrendelesek

## Megrendelések listája
**Hivatalos:** https://unas.hu/tudastar/admin/megrendelesek-listaja
- Szűrés felhasználó / típus / státusz / dátumintervallum szerint; rendezés
  azonosító, dátum, név, státusz szerint.
- **Kereső:** a rendelés adataiban keres (terméknév, cikkszám, megjegyzés,
  tranzakcióazonosító, kuponkód, csomagszám…). Hogy miben keressen:
  `Beállítások / Alapbeállítások / Megrendelés` — minél több mező, annál lassabb.
- Tooltipek a listában (Azonosító / Név / Info oszlop fölé húzva) → sokszor nem
  kell megnyitni a részleteket. Név-ikonok: regisztráció nélküli rendelés; első
  rendelés; van másik nyitott rendelése; van korábbi tartozása; a rendelésben és
  a profilban eltérő adat.

## Megrendelés részletek
**Hivatalos:** https://unas.hu/tudastar/admin/megrendeles-reszletek
- Gombok: Vissza, Nyomtat, Szállítólevél, Elállási nyilatkozat, **Másolás**
  (rendelés duplikálása), **Számlázás** (ha Számlázható státuszú),
  **Újrakalkulál** (szállítási + kezelési költség újraszámítása módosítás után),
  Töröl.
- Három blokk: alapadatok (azonosító, leadás/módosítás ideje, státusz, típus,
  számlázás állapota), tételek, vásárlói/címadatok.
- `Státusz értesítő` gomb: e-mail a vásárlónak státuszváltáskor.

## Megrendelés státuszok, típusok
**Hivatalos:** https://unas.hu/tudastar/admin/megrendeles-statuszok-tipusok
**Menü:** `Beállítások / Vásárlási folyamat / Megrendelés státuszok, típusok`
- Új boltnál a fontosabb státuszok automatikusan létrejönnek; bővíthető,
  sorrend fogd-és-vidd.
- Státusznál beállítható: **"Ebbe váltáskor küldjön automatikus értesítést a
  vásárlónak"** (e-mail és/vagy SMS). Az egyes rendelésnél a jelölőnégyzet még
  felülírja.
- **Rendelés státusz típusa** (raktárkezelést befolyásolja):
  - *Normál Nyitott* — a legtöbb köztes státusz (megérkezett, visszaigazolva…)
  - *Sikeresen lezárult* — teljesült (kiszállítva)
  - *Sikertelenül lezárult* — a vevő nem vette át → a tételek **visszakerülnek a
    raktárba**
  - *Feldolgozáson kívüli* — a tételek nincsenek kifoglalva a raktárból
- Típusok: pl. Webáruház rendelés, Bolti eladás. Paraméterek: megrendelés- és
  vásárló-paraméterek is itt.

## Csomagfeladás / futár
**Hivatalos:** https://unas.hu/tudastar/admin/csomagfeladas
- Kétféle integráció: **fájl alapú** (letöltesz egy fájlt, feltöltöd a futár
  szoftverébe) és **API** (teljesen automata: egy gombbal átadod a rendelést,
  visszajön a **csomagszám**, letölthető a címke; a csomagszám státusz-értesítővel
  továbbküldhető a vevőnek).
- Kezeli az átvételi pontot, csomagautomatát, postán maradót, cserecsomagot.
- Integrálás: szerződés a futárral → `Beállítások / Fizetés, Szállítás,
  Logisztika / Speciális szállítási módok`.
- Napi teendő: `Megrendelések / Csomagfeladás` — szállító cégenként `Letölt`.

## Visszáru kezelés
**Hivatalos:** https://unas.hu/tudastar/admin/visszaru-kezeles
- Bekapcsoláskor létrejön két *Visszáru* típusú státusz (Visszaküldés alatt /
  Visszaküldve); kikapcsoláskor törlődnek.
- Beállítható: alap státusz admin által / vásárló által indított
  visszaküldéshez; milyen státuszba váltáskor generálódjon **visszatérítéses
  kupon** (kell: kuponkezelés bekapcsolva); milyen státuszba váltáskor vonja
  vissza a **pontokat** (kell: pontgyűjtés bekapcsolva).
- "A vásárló indíthat visszaküldést" külön kapcsoló.

## Számlázás, ügyvitel
**Hivatalos:** https://unas.hu/tudastar/admin/szamlazas-ugyvitel
- 40+ számlázóprogram; egy részéhez Unas fejlesztette a kapcsolatot
  (aktiválási díj, Unas support), másokat a szoftvergyártó (külső fejlesztés,
  ott a support). API-n gyakorlatilag bármelyik bekötehető.
- Folyamat: vagy a számlázóprogram kéri le a számlázható rendeléseket, vagy az
  adminból indítod (egyesével a rendelés részletekből, vagy tömegesen).

## Összeszedés
**Hivatalos:** https://unas.hu/tudastar/admin/osszeszedes
- Raktári komissiózó lista. Kell hozzá 4 megrendelés-státusz (Összeszedhető /
  Összeszedés folyamatban / Részben összeszedett / Összeszedve) és egy
  termék-paraméter a tárhelynek. Lista max. rendelésszám + max. tételszám +
  szállítási mód szerint.

## Megrendelések exportálása
**Hivatalos:** https://unas.hu/tudastar/admin/megrendelesek-exportalasa
- Excel export; szűrés fizetési/szállítási mód, vásárló csoport, státusz,
  dátum szerint. Választható: 1 sor = 1 rendelés, vagy 1 sor = 1 rendelés-tétel.

## Beszerzés
`Megrendelések / Beszerzés` — a rendelésekhez szükséges, de hiányzó készlet
alapján beszerzési javaslat/lista a beszállítók felé.
