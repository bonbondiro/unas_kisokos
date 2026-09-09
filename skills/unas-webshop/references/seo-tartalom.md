# SEO, meta, robots.txt, llms.txt, URL-kezelés, tartalmi oldalak

**Főmenü:** `Marketing / Keresőoptimalizálás, SEO` és `Tartalom`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/keresooptimalizalas-seo

## SEO beállítások
**Hivatalos:** https://unas.hu/tudastar/admin/seo-beallitasok
**Menü:** `Marketing / Keresőoptimalizálás, SEO / SEO beállítások`
- Közös META adatok hozzáfűzése az egyénileg megadott / automatikusan generált
  meta adatokhoz (külön kapcsolók).
- META title max. hossz (optimum **60**), description max. (optimum **160**),
  keywords alapból **0** (a Google nem használja → nem kerül a forráskódba).
- **Robots META tag** alapérték: `index/noindex`, `follow/nofollow` — kategória-,
  termék-, plusz oldal szinten felülírható.
- Referrer-policy META tag.

## Egyéb SEO almenük
- **Automatikus SEF és META generálás** (`automatikus-sef-es-meta-generalas`):
  sablonból generált beszédes URL + meta minden termékre/kategóriára.
- **Közös META adatok** (`kozos-meta-adatok`) / **Egyéni META adatok**
  (`egyeni-meta-adatok`).
- **URL-kezelés** (`url-kezeles`): 301 átirányítások, URL-struktúra,
  régi→új URL párok (költözésnél kritikus).
- **robots.txt kezelés** (`robots-txt-kezeles`): a fájl tartalmának szerkesztése
  az adminból.
- **llms.txt kezelés** (`llms-txt-kezeles`): robots.txt-szerű, szabványos fájl
  (llmstxt.org) az LLM-eknek (ChatGPT, Claude, Gemini) a legfontosabb tartalmak
  összefoglalására. Nyelvenként külön tartalom. Kitöltve automatikusan elérhető a
  domain gyökerén. **A Google keresés figyelmen kívül hagyja** — csak akkor
  töltsd ki, ha biztos vagy a helyes beállításban.

## Vélemények és SEO
A termékvélemények strukturált adatként (csillag) beágyazódnak → gazdagabb
Google találat. Lásd `references/marketing-hirlevel.md` (Vélemények).

## Tartalom / plusz oldalak
**Hivatalos:** https://unas.hu/tudastar/admin/tartalom
- **Plusz menük, oldalak** (`plusz-menuk-oldalak`): tetszőleges mélységű
  menüstruktúra. Oldaltípusok: *Belső Normál oldal* (tartalmi elemekből:
  szöveg, képgaléria, blog…), *Landoló oldal* (csak a tartalom, boxok/menük
  nélkül), *Külső Link oldal*. Nyelvenként külön.
- **Tartalmi elem kezelés** (`tartalmi-elem-kezeles`): újrafelhasználható
  tartalomblokkok.
- **Banner-boxok** (`banner-boxok`): pl. ingyenes szállítás sáv, kampány-banner.
- **Szerkeszthető tartalmak** / **Módosítható elemek**: a kinézet fix szövegei.
- **Tárolt űrlapok** (`tarolt-urlapok`): egyedi űrlapok (ajánlatkérés,
  visszahívás) — a beérkező adatok az adminban gyűlnek.
- **Fájlkezelő** (`fajlkezelo`): képek, dokumentumok feltöltése.
- **Hírek, Naptar** (`hirek-naptar`): blog/hír modul + eseménynaptár.

## Kinézet / arculat
`Beállítások / Kinézet, arculat` — kinézet választás/testreszabás, egyedi
kinézet, box-sorrend, arculati elemek, **szkript beszúrás**
(`script-beszuras` — fej/láb kód; feltételes futtatáshoz inkább intelligens
tartalom szkript típus), mobil változat. Fejlesztői részletek:
`references/api.md` (JS API) és https://unas.hu/tudastar/design
