# Elhagyott kosár visszaszerzése — playbook

**Hivatalos oldalak:**
- https://unas.hu/tudastar/admin/elhagyott-kosarak
- https://unas.hu/tudastar/admin/automata-folyamatok
- https://unas.hu/tudastar/admin/koveto-hirlevel

## 1. Mit tud az Unas

| | Követő hírlevél | **Automata folyamatok** (ajánlott) |
|---|---|---|
| Menü | `Marketing / Hírlevél / Követő hírlevél` | `Beállítások / Automata folyamatok` |
| Legkorábbi küldés | **1 nap** | **~5 perc**, perc pontossággal |
| Feltételek | vásárló csoport, "Új vásárló", "Feliratkozott hírlevélre", "Kereső kifejezés" (kosár termékneveiben), termékszűrés | ugyanezek + kosár tételszám / név / ár, összköltés, irányítószám, stb. |
| Sorozat | több sablon, de mind napos lépcső | 1 folyamat = 1 levél; több folyamat = sorozat |
| Elágazás megnyitás/kattintás alapján | nincs | nincs (csak idő-alapú + "rendelt → leáll") |

### Kötelező előfeltételek
- **Szerverre mentett kosár** bekapcsolva: `Beállítások / Alapbeállítások / Működés`.
- **Ismert e-mail cím**: a levél csak akkor megy ki, ha a látogató bejelentkezett
  vásárló, vagy a pénztár első lépésében megadta az e-mailjét.
- Az `Elhagyott kosarak` lista (`Megrendelések` főmenü alatt) mutatja: kosárelhagyás
  dátuma, vásárló e-mail, név, tételszám. Kosarak 1 évig tárolva. Exportálható.

## 2. Ajánlott logika (idő-alapú, 2–3 lépcső)

```
[Kosárba tesz + ismert e-mail]  — minden újabb kosármozgás nullázza az időzítőt
   │
1. FOLYAMAT  kosár elhagyás, időzített +1 óra   → emlékeztető levél
   │
2. FOLYAMAT  kosár elhagyás, időzített +24–48 óra → bizalom/segítség VAGY ösztönző
   │
(3. FOLYAMAT kosár elhagyás, időzített +72 óra   → kedvezmény, határidővel)

Rendelés bármikor → elévülés (kosár elhagyás → megrendelés leadás) → függő levelek leállnak
Minden folyamaton feltétel: "Feliratkozott hírlevélre" = igen  (GDPR)
Kedvezményes levélből csoport-kizárás: viszonteladó / nagyker / klub
```

Döntési szempontok:
- **Első levél +1 óra** — friss a vásárlási szándék, de nem tolakodó.
- **Kedvezmény csak az utolsó levélben** — különben a vásárlók megtanulják
  szándékosan elhagyni a kosarat a kuponért. Előbb próbáld ingyenes szállítás
  emlékeztetővel.
- **"Hányszor futhat maximum"**: hagyd bőven (pl. 999); az elévülés kezeli a
  duplikációt egy kosárcikluson belül.
- Nincs natív "30 naponta max 1 sorozat / vásárló" sapka — ha kell, külön logika.

## 3. Beállítási checklist

1. `Beállítások / Alapbeállítások / Működés` → szerverre mentett kosár **be**.
2. `Beállítások / Alapbeállítások` (Pénztár/Megrendelés szekció) **vagy**
   `Marketing / Hírlevél` → a megrendelési űrlapon jelenjen meg egy **alapból
   üres** hírlevél-feliratkozó jelölőnégyzet (előre bepipálva jogszabálysértő).
3. `Marketing / Hírlevél / Hírlevél sablonok` → készíts 2–3 sablont. Mindben:
   `[name]`, `[product_table]`, és egy nagy CTA gomb ("Vissza a kosaramhoz").
   A `[product_table]` termék-URL-jei visszaállítják a kosarat. Nézd meg, van-e a
   sablonszerkesztőben külön "kosár visszaállítása" gomb a kosárelhagyás sablonhoz.
4. `Beállítások / Automata folyamatok / Hozzáad` — folyamatonként:
   - Aktív: igen · Időzített: igen → 1 óra / 24–48 óra / (72 óra)
   - Esemény típusa: **kosár elhagyás**
   - Szabály: "Feliratkozott hírlevélre" = igen (+ a kedvezményesnél
     csoport-kizárás)
   - Művelet: **Email küldése** → a megfelelő sablon
5. **Teszt:** tegyél terméket a kosárba teszt-e-maillel, ne rendeld meg → jönnie
   kell az 1. levélnek. Másik teszt: rendeld le a kosarat 24 órán belül → a
   2–3. levél **ne** menjen ki (elévülés).
6. Kövesd az `Elhagyott kosarak` listát és a rendelésekben a kuponkód-használatot.

## 4. GDPR

- Az elhagyott kosár e-mail Magyarországon **direkt marketingnek** minősül →
  biztonságos: csak marketing/hírlevél hozzájárulást adott címzettnek küldj.
  Ezért van minden folyamaton a "Feliratkozott hírlevélre = igen" feltétel.
- Minden levél alján `[link_unsubscribe]`.
- "Jogos érdek" alapon nem-feliratkozóknak küldeni szürke zóna — csak adatvédelmi
  szakértő jóváhagyásával.

## 5. Sablonvázak (kiindulás, testre szabandó)

**1. levél (+1 óra) — emlékeztető**
> Tárgy: `Ottmaradt valami a kosaradban` / `[name], megőriztük a kosaradat`
> Szia [name]! Félbemaradt a rendelésed — a kosaradat megőriztük.
> [product_table]
> [GOMB: Vissza a kosaramhoz]
> Kérdés? Válaszolj erre az e-mailre.

**2. levél (+24–48 óra) — bizalom/segítség**
> Tárgy: `Segítsünk a választásban?`
> Eredeti termék, gyári garancia, gyors szállítás, üzlet címe, ügyfélszolgálat.
> [product_table] · [GOMB: Vissza a kosaramhoz]

**3. levél (+72 óra) — ösztönző (A vagy B)**
> A) kedvezmény nélkül: ingyenes szállítás küszöb emlékeztető + [GOMB: Rendelés befejezése]
> B) kedvezménnyel: `[name], –10% a kosaradra 48 óráig` + [KUPONKÓD] + [GOMB: Beváltom]

**B2B változat (a kedvezményes levél helyett):** "Nagyobb tételben vásárolnál?
Kérj egyedi árajánlatot: [telefon] / [e-mail]."
