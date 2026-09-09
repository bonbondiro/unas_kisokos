# Termékek, kategóriák, paraméterek, tömeges módosítás, raktárkezelés, feed import

**Főmenü:** `Termékek`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/termekek

## Kategóriák
**Hivatalos:** https://unas.hu/tudastar/admin/kategoriak-letrehozasa
**Menü:** `Termékek / Kategóriák kezelése`
- Tetszőleges mélységű fa. **Kategóriák száma max. a csomag terméklimitjének
  fele.** Sorrend: ABC vagy kézi (`Beállítások / Alapbeállítások / Kategória`).
- Ugyanitt hozol létre terméket egy kategórián belül (`Új termék`).
- Speciális kategóriák (újdonságok, akciós termékek) külön kezelve.

## Termékek létrehozása
**Hivatalos:** https://unas.hu/tudastar/admin/termekek-letrehozasa
- `Termékek / Kategóriák kezelése` → kategória → `Új termék`. Lapfülek:
  alapadatok, képek, paraméterek, SEO, kapcsolódó/kiegészítő termékek, stb.
- **Cikkszám = azonosító**; `Ment új termékként` csak más cikkszámmal.
- Mentés-variánsok: `Ment majd raktár`, `Ment és marad`, `Ment`.

## Termék paraméterek
**Hivatalos:** https://unas.hu/tudastar/admin/termek-parameterek
**Menü:** `Beállítások / Termék beállítások / Termék paraméterek`
- Típusok: szabad szavas; szabad szavas többértékű (TAG, vesszős, szűrésnél
  ÉS/VAGY); **értékkészlet** (fix lista, elgépelés-védett — a tömeges feltöltésnél
  fontos); értékkészlet többértékű; szám; (továbbá kép, link, dátum stb.).
- **Figyelem:** értékkészlet típusban a gyorskereső nem keres.
- Használat: összehasonlítás, szűrés-box, ár-összehasonlító feed speciális
  mezői (Gyártó, ISBN, Szállítási idő…).

## Termék státuszok
**Hivatalos:** https://unas.hu/tudastar/admin/termek-statuszok
- Max. 3 egyéb státusz (pl. Előrendelhető, Outlet, Kiemelt). Szűrhető a
  kategóriában, ha engedélyezed: `Beállítások / Alapbeállítások / Működés` →
  szűrés-box beállítás. Többnyelvűnél nyelvenként.

## Csoportos módosítás
**Hivatalos:** https://unas.hu/tudastar/admin/csoportos-modositas
- Egy kategória összes termékének **ugyanazon** paraméterét ugyanazzal az
  értékkel/aránnyal módosítja (pl. nettó ár +5%, ÁFA-kulcs csere). Először példát
  mutat egy terméken, aztán végrehajt. Főkategória választása = minden benne
  lévő termék.

## Listás módosítás
**Hivatalos:** https://unas.hu/tudastar/admin/listas-modositas
- Leszűrt listában **egyenként eltérő** értékek írhatók: ár, készlet, státusz,
  tömeg. Lista-módok: egy kategóriában lévő / kép nélküli / keresés eredménye /
  véleménnyel rendelkező / raktárkezelésben kezelt-nem kezelt / készlethiányos.
- Változatok készletét itt NEM lehet — `Termékek / Kategóriák kezelése`.

## Raktárkezelés
**Hivatalos:** https://unas.hu/tudastar/admin/raktarkezeles
- Termék sorában `Raktár` gomb. Itt kapcsolható be a raktárkezelés a termékre,
  és hogy vásárolható-e készlethiánynál. Főraktár készlet közvetlenül átírható;
  részletes mozgás: **Betesz / Kivesz** (raktárcímke, beszállító megadható).
- `Előzmények törlése` összevonja a mozgásokat — **nem visszavonható**.
- Csomagtermék készlete az összetevőkből számítódik.
- Készlet megjelenítése a vásárlói felületen: `Beállítások / Alapbeállítások /
  Megjelenés`.
- Kapcsolódó almenük: raktárkészlet-statisztika, raktárkészlet-adatbázis
  (export/import), raktárcímkék, további raktárak, raktárkészlet-intervallumok
  (készlet-sáv szöveg: „raktáron", „1-2 db"…), beszállítók, felvételi helyek.

## Automata import, feed bekötés
**Hivatalos:** https://unas.hu/tudastar/admin/automata-termek-import
- Külső adatforrásból (pl. nagykereskedelmi feed) napi/heti termék- és
  ár-frissítés, új termék felvitel, képek. **Egyedi fejlesztés** (formátum-
  konverziós modul) + üzemeltetési díj (terméklimit + gyakoriság függvénye).
  Az Unas előzetesen egyeztet az igényről.
- Alternatíva saját integrációra: `setProduct` / `setProductDB` API
  (`references/api.md`).

## Termék adatbázis export/import
`Termékek / Termék adatbázis` — teljes termékkör Excel/CSV export és
visszatöltés; fizetési/szállítási mód tiltás, vásárló csoport láthatóság az
"Azonosító a Webáruházban" mezőkkel hivatkozva.
