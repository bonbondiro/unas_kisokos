# Kedvezmények, akciók, pontgyűjtés, utó- és csomagajánlat

**Főmenü:** `Marketing` (Kedvezmények szekció)
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/kedvezmenyek

Alapszabály: ha több kedvezmény típus is teljesül egy vásárlóra, jellemzően a
**nagyobb** érvényesül (nem összeadódik) — kivéve, ahol a leírás mást mond
(pl. vásárló csoport közvetlen + végösszeg kedvezmény együtt hat).

## Kuponok, ajándékkártyák — `Marketing / Kuponok, ajándékkártyák`
**Hivatalos:** https://unas.hu/tudastar/admin/kuponok-ajandekkartyak
- **Végösszeg kedvezmény kupon:** összegszerű vagy százalékos; érvényességi idő;
  minimum vásárlási összeg. Százaléknál az alap a termékek eladási ára +
  esetleges közvetlen termékkedvezmény.
- **Termék kedvezmény kupon:** konkrét termékekre / kategóriákra.
- **Ingyenes szállítás kupon** is generálható.
- Beállítható: hányszor használható fel, meddig érvényes, összeghatár.
- Terjesztés: hírlevélben, nyomtatva, offline.

## Ajándéktermékek — `Marketing / Ajándéktermékek`
**Hivatalos:** https://unas.hu/tudastar/admin/ajandektermekek
- `Ajándéktermék használata` kapcsoló. Szabályonként: megnevezés, **kosárérték**
  küszöb (bruttó), kosárérték-számítás alapja (teljes kosár VAGY csak az
  "Ezekhez adható ajándék" termékek értéke — utóbbi márkaspecifikus akcióhoz).
- Az ajándék a rendelésben külön 0 értékű tételként jelenik meg (raktár- és
  számlabarát). Több ajándékakció futhat párhuzamosan; a rendszer a kosár
  alapján mutatja a választható ajándékokat.
- Ha van kosárérték-küszöb, az ajándékválasztás csak a kosár oldalon jelenik meg,
  a termékadatlapon nem.

## Mennyiségfüggő akciók — `Marketing / Mennyiségfüggő akciók`
**Hivatalos:** https://unas.hu/tudastar/admin/mennyisegfuggo-akciok
- "1-et fizet 2-t kap" és minden variánsa. A jogosító és az ajándék/kedvezményes
  termék lehet különböző. Mezők: megnevezés, érvényességi idő, kedvezmény
  mértéke, rendelésenkénti felhasználás max., "Ki veheti igénybe?" (regisztrált /
  új / hírlevél-feliratkozó), vásárló csoport, "Ezekhez használható fel"
  (termékek/kategóriák + min. darab), "Ezekből választható" (termékek/kategóriák
  + darab).

## Időszakos árváltozás — `Marketing / Időszakos árváltozás`
**Hivatalos:** https://unas.hu/tudastar/admin/idoszakos-arvaltozas
- Előre ütemezett akciók/áremelések (Black Friday, hétvégi akció, ünnep).
  Mezők: megnevezés, **publikus időszak**, **megjelenés periódusa** (ismétlődő,
  napra/hónapra/hét napjára, óra-percre, nyitvatartás és munkaszüneti napok
  figyelembevételével), mérték (%), **irány** (negatív = akció, pozitív =
  áremelés), árszámítás alapja (normál vagy egyedi akciós ár), vásárló csoport.
- **Figyelem:** időszakos árcsökkentés NEM teszi a terméket a "speciális akciós"
  kategóriába, és nem vált ki árcsökkenés-értesítőt.

## Kosárérték kedvezmény — `Marketing / Kosárérték kedvezmény`
**Hivatalos:** https://unas.hu/tudastar/admin/kosarertek-kedvezmeny
- **Kosárérték alapján sávos %:** pl. 100 000 Ft felett 2% a végösszegből.
  Sávok szabadon. Vásárló csoportonként külön sáv; az alap sáv a többi
  csoportra érvényes.
- **Korábbi rendelések alapján sávos %:** az eddigi rendelések összege alapján
  extra % (az aktuális rendelés nem számít bele). Csoportonként külön.
- Vásárló csoportnál külön tiltható/engedélyezhető, hogy jár-e kosárérték-alapú
  kedvezmény (pl. nagykernek ne).
- **Kosárérték alapján csoportár** is van (más csoport árait kaphatja meg a vevő
  adott kosárérték felett).

## Pontgyűjtés — `Marketing / Pontgyűjtés`
**Hivatalos:** https://unas.hu/tudastar/admin/pontgyujtes
- 1 pont = 1 pénznemegység. Beállítható: pontgyűjtés ki/be, regisztrációért /
  hírlevél-megerősítésért járó pont, alap felhasználási beállítás
  ("Felhasználom" / "Nem"), akciós termékre jár-e pont (és %-os generálásnál),
  a végösszeg hány %-áig fedezhető pontból, alap pontérték a termék bruttó ára
  után, pont lejárat.
- Kombinálható a hírlevéllel: pont lejárata előtt emlékeztető ("van összeg a
  pont egyenlegen" feltétellel).

## Utóajánlat — `Marketing / Utóajánlat`
**Hivatalos:** https://unas.hu/tudastar/admin/utoajanlat
- A **rendelés leadása utáni köszönőoldalon** időzítve felugró egyetlen
  termékajánlat; egy kattintással a már leadott rendeléshez kerül. A termékeknél
  beállított **kiegészítő termékeket** használja.
- Mezők: használat ki/be; kupon-/pontfelhasználás esetén elérhető-e; költségek
  újrakalkulálása elfogadáskor; hány másodperc után jelenjen meg (egész szám);
  utóajánlat-specifikus extra **kedvezmény %** (egész szám); melyik kiegészítő
  termék (legelső / legutolsó / véletlen); vásárló csoport; fizetési mód
  szűrés.
- Nem rombolja a konverziót, mert a vásárlás már megtörtént.

## Csomagajánlat — `Marketing / Csomagajánlat`
**Hivatalos:** https://unas.hu/tudastar/admin/csomagajanlat
- Együtt vásárolt termékekből dinamikus árú csomag a termékadatlapon (nem kell
  külön cikkszám, mint a csomagterméknél; a számlán külön tételek).
- `Használom a csomagajánlat funkciót` kapcsoló; max. hány ajánlat a
  termékadatlapon. Ajánlatonként: aktív, érvényességi idő, **árképzés típusa**
  (normál/akciós árból összegszerű vagy százalékos kedvezmény, vagy fix ár).

## Vásárló csoport kedvezmények
Lásd `references/vasarlok-csoportok.md` — közvetlen % a termékárból + végösszeg %
+ minimum rendelési összeg + kosárérték-kedvezmény tiltás/engedélyezés
csoportonként.
