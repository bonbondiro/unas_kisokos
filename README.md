# unas-webshop

Szakértői tudásbázis-**skill** az [Unas](https://unas.hu) bérelhető
webáruház-rendszerhez. Egy helyre gyűjti, hogyan működnek az Unas admin
funkciói, a marketing- és automatizmus-logika (hírlevél, követő hírlevél,
automata folyamatok, kedvezmények), az elhagyott kosár visszaszerzése, a
termék- és rendeléskezelés, valamint az XML API — mindig a hivatalos
`unas.hu/tudastar` oldalra mutató linkkel.

A cél: bármely AI-asszisztens (Claude Code, Cursor, más SKILL.md-t olvasó
eszköz) az Unas webshopon dolgozva ne kezdje nulláról, hanem legyen kész
mentális térképe a rendszerről.

## Mit tartalmaz

```
unas-webshop/
├── .claude-plugin/
│   ├── plugin.json          # Claude Code plugin manifest
│   └── marketplace.json     # hogy /plugin-nel telepíthető legyen
└── skills/
    └── unas-webshop/
        ├── SKILL.md         # router: mikor mit, + rendszer-szintű fogalmak
        └── references/
            ├── admin-map.md              # a teljes tudástár témakör-térképe + URL-ek
            ├── automata-folyamatok.md    # esemény→feltétel→művelet, elévülés, webhook
            ├── elhagyott-kosar.md        # teljes kosár-visszaszerzés playbook + GDPR
            ├── marketing-hirlevel.md     # hírlevél, feliratkozók, SMS/push, intelligens tartalom
            ├── kedvezmenyek.md           # kupon, pont, ajándék, BOGO, időszakos ár, csomagajánlat
            ├── ertesitesek-cseremezok.md # rendszer-e-mailek + a cseremezők (merge fields) teljes listája
            ├── megrendelesek.md          # rendelés, státuszok, futár, visszáru, számlázás
            ├── termekek-keszlet.md       # termék, kategória, paraméter, tömeges módosítás, raktár, feed
            ├── vasarlok-csoportok.md     # vásárló adatlap, csoportok, import/export
            ├── beallitasok-vasarlas.md   # alapbeállítás, pénztár, fizetés/szállítás, nyelv, jog/GDPR
            ├── seo-tartalom.md           # SEO, meta, robots.txt, llms.txt, plusz oldalak
            ├── kulso-kapcsolatok.md      # API kulcs, Facebook/Google, piacterek, feed, statisztika
            └── api.md                    # XML API: azonosítás, limitek, végpontlista, JS API
```

## Telepítés

### A) Claude Code plugin (marketplace-ből)

```bash
/plugin marketplace add /eleresi/ut/unas-webshop
/plugin install unas-webshop@unas-webshop-marketplace
```

Vagy tedd egy git repóba, és a repo URL-jét add meg a `marketplace add`-nek.

### B) Csak a skill (bármely eszközhöz)

Másold a `skills/unas-webshop/` mappát a saját skill-könyvtáradba:

- Claude Code: `~/.claude/skills/unas-webshop/`
- projekt-szintű: `<projekt>/.claude/skills/unas-webshop/`
- más eszköz: ahova az a `SKILL.md` alapú skilleket várja

A `SKILL.md` sima Markdown, nincs benne eszközfüggő mechanika, csak a
`references/` fájlokra hivatkozik relatív úton.

## Használat

A skill triggerelődik, amint Unas webshopról esik szó ("a webáruházamban…",
"elhagyott kosár", "hírlevél automatizmus", unas.hu link, stb.). Ezután a
`SKILL.md` témakör-térképe alapján beolvassa a releváns `references/` fájlt, és
ha kell, lekéri a hivatkozott hivatalos tudástár-oldalt az élő részletekért.

## Forrás és jogi megjegyzés

A `references/` fájlok **saját szavas összefoglalók** a nyilvánosan elérhető
`https://unas.hu/tudastar/` tartalom alapján, tanulási/segéd céllal. Nem az
Unas dokumentáció szó szerinti másolata. A hiteles, naprakész forrás mindig a
hivatalos tudástár és a felhasználó saját admin felülete. Az Unas és a
tudástár tartalma az UNAS Online Kft. tulajdona.

## Karbantartás

Az Unas rendszeresen fejleszt; a számok, limitek, menünevek változhatnak. Ha
eltérést látsz, javítsd az adott `references/` fájlt, és a sor alján hagyd meg a
hivatalos URL-t, hogy ellenőrizhető maradjon.
