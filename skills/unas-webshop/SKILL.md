---
name: unas-webshop
description: >-
  Unas (unas.hu) webáruház-rendszer szakértői segéd. Használd MINDIG, amikor Unas
  webshopról van szó: admin beállítás, marketing (hírlevél, követő hírlevél,
  automata folyamatok, kedvezmény, kupon, pontgyűjtés), elhagyott kosár
  visszaszerzése, termék- és készletkezelés, megrendelés- és számlázási folyamat,
  vásárló csoportok, SEO/meta/llms.txt, fizetési-szállítási módok, vagy az Unas
  XML API / webhook / JS API integráció. Akkor is hívd, ha a felhasználó csak
  annyit mond, hogy "a webshopomban" és a kontextusból Unas derül ki, vagy ha
  unas.hu linket ad. Use this whenever the user works with an Unas webshop:
  admin configuration, abandoned-cart recovery, newsletters and automation,
  discounts, products/stock, orders/invoicing, or the Unas API.
---

# Unas webáruház — szakértői segéd

Ez a skill az Unas bérelhető webáruház-rendszer (unas.hu) admin felületének és
API-jának ismeretét adja. Az Unas Magyarország egyik legnagyobb webshop-motorja;
a teljes dokumentáció a **https://unas.hu/tudastar/** címen érhető el, és a skill
minden témához belinkeli a pontos hivatalos oldalt, ahonnan élő részletet lehet
lekérni (`WebFetch` vagy böngésző — a `<article>` tartalom szerver-oldalon
renderelt, sima `fetch()` is visszaadja).

## Hogyan dolgozz ezzel a skill-lel

1. **Azonosítsd, melyik területről van szó** (lásd a témakör-térképet lent), és
   olvasd be a hozzá tartozó `references/` fájlt — ezek tömör, gyakorlati
   jegyzetek: mit csinál a funkció, hol van az admin menüben, mik a korlátai és a
   tipikus buktatók.
2. **Ha a pontos mezők/limitek kellenek**, kérd le a `references` fájl alján
   megadott hivatalos tudástár-URL-t. A skill jegyzetei szándékosan rövidek; a
   hiteles forrás mindig a tudástár.
3. **Konkrét beállításnál** mindig a menüutat add meg a felhasználónak
   (`Beállítások / Automata folyamatok`), és javasolj tesztelési lépést, mert az
   Unas sok funkciója csomag-szinttől (STANDARD / PREMIUM / VIP) függ, és nem
   minden webshopban van minden bekapcsolva.

## Átfogó, rendszer-szintű fogalmak (ezeket ismerd fejből)

- **Csomag-szintek.** STANDARD / PREMIUM / VIP. Sok limit (termékszám,
  hírlevélkeret, API-óradíj, funkció-elérés) ettől függ. Ha egy funkció "nincs
  ott" a felhasználónál, elsőként a csomagot és a kapcsolót nézd.
- **Szerverre mentett kosár.** Több marketing-funkció (elhagyott kosár, követő
  hírlevél kosárra) előfeltétele. Kapcsoló: `Beállítások / Alapbeállítások /
  Működés`.
- **Vásárló csoportok** (`Megrendelések / Vásárlók / Vásárló csoportok`).
  Központi szegmentáló eszköz: külön ár, közvetlen % kedvezmény, végösszeg-%,
  minimum rendelési összeg, kosárérték-kedvezmény tiltás/engedélyezés,
  hírlevél-célzás, automata folyamat feltétel. B2B (nagyker, viszonteladó, klub)
  jellemzően külön csoport. Nem bejelentkezett / vendég vásárlónak nincs
  csoportja.
- **Cseremezők (`[name]`, `[product_table]`, `[url_payment]`, …).** Az összes
  értesítő- és hírlevél-sablon ezekkel dolgozik. A teljes lista és a
  "melyik esemény­nél melyik érhető el" szabály:
  `references/ertesitesek-cseremezok.md`.
- **Két automatizálási réteg:**
  - *Követő hírlevél* — egyszerű, **min. 1 nap** késleltetés.
  - *Automata folyamatok* — esemény → feltétel → művelet, **perc pontossággal**,
    ~5 perctől; webhook és vásárlócsoport-átsorolás is művelet lehet.
- **Nyelvek.** Többnyelvű bolt esetén szinte minden szöveg (termék, kategória,
  sablon, szállítási mód) nyelvenként külön kitöltendő; a hírlevél/követő
  hírlevél nyelv szerint szűrhető. Külön ország-oldal = külön Unas webáruház,
  saját adminnal.
- **Export/import azonosítók.** Fizetési mód, szállítási mód, vásárló csoport
  mind "Azonosító a Webáruházban" mezővel hivatkozható a termék-adatbázis
  export/importban.
- **API.** XML alapú, `getX`/`setX` végpárok, token 2 órán át él, óradíj-limit
  csomagfüggő. Részletek: `references/api.md`.

## Témakör-térkép — melyik reference fájlt olvasd

| Ha erről van szó | Olvasd |
|---|---|
| Teljes admin-struktúra, "hol van az a menü", bármely tudástár-oldal URL-je | `references/admin-map.md` |
| Hírlevél sablon, hírlevél küldés, feliratkozók, külső hírlevélküldő, SMS, push, intelligens tartalom (felugró/beúszó), partnerprogram, vélemények | `references/marketing-hirlevel.md` |
| Automata folyamatok: események, feltételek, elévülés, műveletek, időzítés, webhook | `references/automata-folyamatok.md` |
| Elhagyott kosár visszaszerzése (teljes playbook, GDPR, sablonvázak, beállítási checklist) | `references/elhagyott-kosar.md` |
| Kupon, végösszeg-/termékkedvezmény, ajándéktermék, mennyiségfüggő akció, időszakos árváltozás, kosárérték-kedvezmény, pontgyűjtés, utóajánlat, csomagajánlat | `references/kedvezmenyek.md` |
| Rendszer-értesítők (email/SMS), és a cseremezők (merge fields) teljes referenciája | `references/ertesitesek-cseremezok.md` |
| Megrendelés lista/részletek, státuszok és típusok, csomagfeladás/futár, visszáru, számlázás, összeszedés, export | `references/megrendelesek.md` |
| Termék és kategória létrehozás, termék paraméterek, termék státuszok, csoportos/listás módosítás, raktárkezelés, automata termékimport/feed | `references/termekek-keszlet.md` |
| Vásárló létrehozás/adatlap, vásárló csoportok, vásárló export/import | `references/vasarlok-csoportok.md` |
| Alapbeállítások, vásárlási folyamat, fizetési és szállítási módok + kapcsolásuk, pénznemek, nyelvek, ÁSZF/adatkezelés/GDPR, cookie-sáv | `references/beallitasok-vasarlas.md` |
| SEO, közös/egyedi meta, automata SEF+meta, robots.txt, llms.txt, URL-kezelés, plusz oldalak/menük, banner-boxok, tárolt űrlapok | `references/seo-tartalom.md` |
| API kulcs, Facebook pixel + Konverziók API, Google Analytics/Ads, piacterek (eMAG, Árukereső, Allegro), árösszehasonlító feed, statisztika | `references/kulso-kapcsolatok.md` |
| Unas XML API, azonosítás, limitációk, végpontlista, webhook-igazolás, JavaScript API | `references/api.md` |

## Fontos figyelmeztetés a forrásról

A `references/` fájlok saját szavas összefoglalók a nyilvános
`unas.hu/tudastar` alapján — **nem** az Unas dokumentáció szó szerinti másolata.
Számok, limitek, mezőnevek változhatnak; éles tanács előtt ellenőrizd a
belinkelt hivatalos oldalon. A felhasználó admin felülete az igazság forrása:
ha egy leírt kapcsoló nincs ott, az csomag- vagy verziókérdés lehet.
