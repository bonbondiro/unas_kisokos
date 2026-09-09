# Unas kisokos — teljes egybefűzött változat

Ez a fájl az Unas (unas.hu) webáruház-rendszer működésének összefoglalója, egyetlen
dokumentumban. Töltsd fel egy AI-projekt tudásanyagának (Claude Projects, ChatGPT
Projects, NotebookLM), és onnantól minden beszélgetésben elérhető.

Forrás: saját szavas összefoglaló a nyilvános https://unas.hu/tudastar/ alapján;
minden fejezetben ott a hivatalos link a részletekhez. Hiteles forrás mindig a
tudástár és a saját admin felület.

Repo (frissülő verzió + telepíthető plugin): https://github.com/bonbondiro/unas_kisokos

---


# 0. Áttekintés és témakör-térkép (SKILL.md)


### Unas webáruház — szakértői segéd

Ez a skill az Unas bérelhető webáruház-rendszer (unas.hu) admin felületének és
API-jának ismeretét adja. Az Unas Magyarország egyik legnagyobb webshop-motorja;
a teljes dokumentáció a **https://unas.hu/tudastar/** címen érhető el, és a skill
minden témához belinkeli a pontos hivatalos oldalt, ahonnan élő részletet lehet
lekérni (`WebFetch` vagy böngésző — a `<article>` tartalom szerver-oldalon
renderelt, sima `fetch()` is visszaadja).

### Hogyan dolgozz ezzel a skill-lel

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

### Átfogó, rendszer-szintű fogalmak (ezeket ismerd fejből)

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

### Témakör-térkép — melyik reference fájlt olvasd

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

### Fontos figyelmeztetés a forrásról

A `references/` fájlok saját szavas összefoglalók a nyilvános
`unas.hu/tudastar` alapján — **nem** az Unas dokumentáció szó szerinti másolata.
Számok, limitek, mezőnevek változhatnak; éles tanács előtt ellenőrizd a
belinkelt hivatalos oldalon. A felhasználó admin felülete az igazság forrása:
ha egy leírt kapcsoló nincs ott, az csomag- vagy verziókérdés lehet.


---


# 1. Teljes tudástár témakör-térkép

### Unas tudástár — teljes témakör-térkép

Minden téma egy sora: **slug — egymondatos leírás**. A hivatalos oldal:
`https://unas.hu/tudastar/admin/<slug>` (kivéve ahol más prefix van jelölve).
Ha részlet kell (mezők, limitek), kérd le a megfelelő URL-t (`fetch()` /
`WebFetch` — az `<article>` szerver-oldalon renderelt).

A mélyebb, saját szavas jegyzetek a testvér-fájlokban vannak — a "→" mutatja,
melyikben.

---

### Megrendelések (főmenü)

| slug | leírás |
|---|---|
| `megrendelesek` | a rendeléskezelés gyűjtő oldala → `megrendelesek.md` |
| `megrendelesek-listaja` | beérkezett rendelések listája, szűrés, kereső, tooltipek |
| `megrendeles-reszletek` | egy rendelés részletei, funkciógombok (nyomtat, számláz, újrakalkulál, másol) |
| `elhagyott-kosarak` | félbehagyott kosarak listája (1 évig), export → `elhagyott-kosar.md` |
| `osszeszedes` | raktári komissiózó lista 4 státusz + tárhely-paraméter alapján |
| `beszerzes` | hiányzó készlet alapján beszerzési lista a beszállítóknak |
| `termek-elofizetesek` | ismétlődő (subscription) termékrendelések kezelése |
| `megrendelesek-exportalasa` | rendelések Excel export (1 sor = rendelés vagy tétel) |
| `csomagfeladas` | futárintegráció (fájl / API), címke, csomagszám → `megrendelesek.md` |
| `szamlazas-ugyvitel` | 40+ számlázóprogram bekötése, tömeges/egyedi számlázás |

#### Megrendelések / Vásárlók → `vasarlok-csoportok.md`
`vasarlok-kezelese`, `vasarlok-listaja`, `vasarlo-adatlap`, `vasarlo-adatbazis`
(export/import), `vasarlo-csoportok`.

---

### Termékek (főmenü) → `termekek-keszlet.md`

| slug | leírás |
|---|---|
| `termekek` | termékkezelés gyűjtő oldala |
| `kategoriak-letrehozasa` | fő-/alkategória fa (max. terméklimit fele) |
| `specialis-kategoriak-kezelese` | újdonságok, akciós, kiemelt stb. dinamikus kategóriák |
| `kategoria-adatbazis` | kategóriák tömeges export/import |
| `kategoria-kepek` | kategóriaképek kezelése |
| `termekek-letrehozasa` | termék adatlap, lapfülek, mentés-variánsok |
| `termek-adatbazis` | teljes termékkör Excel/CSV export–import |
| `termek-kepek` | termékképek tömeges kezelése |
| `termek-osszevonas` | duplikált termékek összevonása |
| `listas-modositas` | leszűrt listában egyenkénti ár/készlet/státusz szerkesztés |
| `termekek-keresese` | termékkereső az adminban |
| `csoportos-modositas` | egy kategória összes termékének azonos módosítása (pl. +5% ár) |

#### Termékek / Raktárkezelés
`raktarkezeles`, `raktarkeszlet-statisztika`, `raktarkeszlet-adatbazis`,
`raktarcimkek`, `tovabbi-raktarak`, `raktarkeszlet-intervallumok`
(készlet-sáv szöveg), `beszallitok`, `felveteli-helyek`,
`automata-termek-import` (feed, egyedi fejlesztés).

---

### Marketing (főmenü)

#### Hírlevél, SMS, push → `marketing-hirlevel.md`
`hirlevel`, `hirlevel-szerkesztes` (sablon + cseremezők), `hirlevel-kuldes`
(keret, célközönség), `koveto-hirlevel` (min. 1 nap, kosárelhagyás is),
`feliratkozok-listaja`, `feliratkozo-adatbazis`, `kulso-hirlevelkuldo`,
`sms` / `sms-sablonok` / `sms-kuldes` / `sms-hirlevel-egyenleg(-feltoltes)`,
`push-uzenetek` / `push-sablonok` / `push-kuldes`, `intelligens-tartalom`
(felugró/beúszó, feltételrendszer), `partnerprogram` (affiliate).

#### Kedvezmények → `kedvezmenyek.md`
`kedvezmenyek`, `kuponok-ajandekkartyak`, `ajandektermekek`,
`mennyisegfuggo-akciok`, `idoszakos-arvaltozas`, `kosarertek-kedvezmeny`,
`pontgyujtes`, `utoajanlat`, `csomagajanlat`.

#### Egyéb marketing
| slug | leírás |
|---|---|
| `marketing` | marketing gyűjtő oldala |
| `hirek-naptar` | blog/hír modul + eseménynaptár |
| `kulso-marketing-rendszerek` | hőtérkép, session replay, prediktív kereső, automatizáló platformok |
| `nyomtathato-arlista` | PDF árlista generálás |
| `velemeny-szavazas-forum` / `velemeny` / `szavazas` / `forum` | termékvélemény (csillag, SEO), szavazás, fórum modul |
| `partnerprogram` | affiliate (fent is) |

#### Keresőoptimalizálás, SEO → `seo-tartalom.md`
`keresooptimalizalas-seo`, `seo-beallitasok`, `automatikus-sef-es-meta-generalas`,
`kozos-meta-adatok`, `egyeni-meta-adatok`, `url-kezeles`, `robots-txt-kezeles`,
`llms-txt-kezeles`.

---

### Tartalom (főmenü) → `seo-tartalom.md`
`tartalom`, `plusz-menuk-oldalak`, `tartalmi-elem-kezeles`, `banner-boxok`,
`szerkesztheto-tartalmak`, `tarolt-urlapok`, `fajlkezelo`.

---

### Statisztika, Napló, Elemzés (főmenü) → `kulso-kapcsolatok.md`
`statisztika-naplo-elemzes`, `latogatasi-statisztika`, `termek-statisztika`,
`termek-feliratkozasok`, `megrendeles-statisztika`, `admin-naplo`,
`hatterfolyamat-naplo`, `vasarlo-naplo`, `api-naplo`, `kulso-statisztikak`.

---

### Beállítások (főmenü)

#### Alapbeállítások → `beallitasok-vasarlas.md`
`beallitasok`, `alapbeallitasok` (lapfülek: Kategória / Termék / Vásárló /
Megrendelés / **Működés** [szerverre mentett kosár!] / Megjelenés / Marketing).

#### Pénznemek, Árkijelzés
`penznemek-arkijelzes`, `penznemek`, `afa-beallitasok`, `arkijelzes`.

#### Szövegek, Nyelvek
`szovegek-nyelvek`, `nyelvek-beallitasa`, `alap-szovegek`.

#### Kinézet, arculat (→ részletek: `https://unas.hu/tudastar/design`)
`kinezet-arculat`, `kinezet-kivalasztasa`, `kinezet-testreszabasa`,
`egyedi-kinezet`, `oldal-kinezetek`, `modosithato-elemek`,
`ajanlok-top-termekek`, `box-sorrend-modositas`, `arculati-elemek`,
`script-beszuras`, `mobil-valtozat`.

#### Fizetés, Szállítás, Logisztika → `beallitasok-vasarlas.md`, `megrendelesek.md`
`fizetes-szallitas-logisztika`, `fizetesi-modok`,
`bankkartyas-specialis-fizetesi-modok` (Barion, SimplePay, OTP, PayPal,
áruhitel), `szallitasi-modok`, `specialis-szallitasi-modok` (futár API-k),
`szallitasi-koltsegek`, `szallitas-es-fizetes-kapcsolas`,
`szallitasi-teruletek-kezelese`, `atveteli-pontok-kezelese`,
`orszagok-kezelese`, `kiszervezett-logisztika` (3PL/fulfilment).

#### Termék beállítások → `termekek-keszlet.md`
`termek-beallitasok`, `termek-parameterek`, `termek-plusz-adatok`,
`termek-statuszok`, `plusz-szolgaltatasok`, `matricak`, `keresesi-beallitasok`.

#### Vásárlási feltételek (jog) → `beallitasok-vasarlas.md`
`vasarlasi-feltetelek`, `altalanos-szerzodesi-feltetelek`,
`adatkezelesi-tajekoztato`, `kulso-aszf-megoldasok`, `adatkezelesi-beallitasok`
(cookie, GDPR, profilalkotás), `vasarlasi-tudnivalok`, `elallasi-nyilatkozat`.

#### Vásárlási folyamat → `megrendelesek.md`, `ertesitesek-cseremezok.md`
`vasarlasi-folyamat`, `megrendeles-statuszok-tipusok`, `megrendeles-parameterek`,
`megrendeles-torles`, `gyorsrendeles`, `vasarlo-parameterek`, `ertesitesek`
(rendszer-e-mailek + cseremezők), `visszaru-kezeles`, `email-ellenorzes`,
`cim-ellenorzes`, `cimkek`.

#### Automata folyamatok → `automata-folyamatok.md`
`automata-folyamatok` (esemény → feltétel → művelet, perc pontos, webhook).

#### Külső kapcsolatok → `kulso-kapcsolatok.md`, `api.md`
`kulso-kapcsolatok`, `api-kapcsolat` (API kulcs, HMAC), `facebook-kapcsolatok`
(pixel + CAPI), `google-kapcsolatok` (GA4, Ads), `kozossegi-media`,
`piacterek` (+ `-unasplaza`, `-arukereso-marketplace`, `-emag-marketplace`,
`-allegro`, `-wolt`), `arosszehasonlito-export-feed`, `chat-a-latogatoval`,
`minosito-rendszerek`.

#### Egyéb beállítások
| slug | leírás |
|---|---|
| `ssl-beallitas` | SSL tanúsítvány |
| `webalkalmazas` | PWA bekapcsolás (push előfeltétele) |
| `webaruhazak-szinkronizalasa` | több Unas bolt közti szinkron |
| `tartalom-vedelem` / `termekkepek-vizjelezese` / `ip-tiltas` / `masolas-vedelem` | tartalomvédelem |
| `webaruhaz-adatai` / `kereskedo-adatai` | cég- és bolt-adatok (`[shop_data]`) |
| `nyitvatartas` / `munkaszuneti-nap-kezeles` | nyitvatartás, ünnepnapok |
| `felhasznalo-jelszo` | admin felhasználók, jogosultságok, jelszó |
| `tamogatas` / `hirek` / `figyelmeztetesek` / `hibabejelentes` | support, rendszerüzenetek |
| `webaruhaz-koltozes` | másik rendszerből költözés |
| `automata-termek-import` | feed import (fent, Termékeknél is) |
| `domain-az-aruhazhoz` / `elofizetes-modositasa` | domain, csomag |

---

### Más tudástár szekciók (nem `/admin/` prefix)

| Szekció | URL prefix | Tartalom |
|---|---|---|
| API dokumentáció | `https://unas.hu/tudastar/api/...` | XML API: azonosítás, limitációk, végpontok (`get*`/`set*`), adatszerkezetek, példák, webhook-ellenőrzés → `api.md` |
| Kinézet dokumentáció | `https://unas.hu/tudastar/design/...` | sablon alapelemei, boxok, oldaltartalmak, beágyazott elemek, `main.cfg` változók, stíluslapok, JS API, sablonszerkesztő |
| Ügyfélfiók | `https://unas.hu/tudastar/ugyfelfiok/...` | pénzügyek, szolgáltatások, domain, felhasználók, előfizető, partnerprogram (ügyfélfiók szint) |
| Integráció (fejlesztőknek) | `https://unas.hu/tudastar/integracio/...` | alkalmazás-integráció: első lépések, telepítés, törlés, demó |
| Hosting / Webtárhely | `https://unas.hu/tudastar/hosting/...` | domain, DNS, aldomain, SSL, e-mail fiók/továbbító/szűrés, FTP, MySQL/phpMyAdmin, ütemezett feladatok, naplók |
| Rendelés (előfizetés) | `https://unas.hu/tudastar/rendeles/...` | tesztáruház nyitás, webáruház-előfizetés, domain/webtárhely rendelés |


---


# 2. Automata folyamatok

### Automata folyamatok

**Menü:** `Beállítások / Automata folyamatok` → `Hozzáad`
**Hivatalos:** https://unas.hu/tudastar/admin/automata-folyamatok
**API-ból is kezelhető:** `getAutomatism` / `setAutomatism` (lásd `api.md`)

Esemény → (feltételek) → művelet. Ezzel váltható ki a legtöbb "ha X történik,
küldj levelet / hívj webhookot / sorold át a vásárlót" automatizmus. Erősebb és
gyorsabb, mint a *Követő hírlevél*.

### A folyamat mezői

| Mező | Jelentés |
|---|---|
| **Aktív** | Ki/be. Inaktívan az esemény nem vált ki műveletet. |
| **Időzített** | Ki: az esemény után azonnal (max ~5 perc). Be: megadható perc / óra / nap késleltetés az esemény után. Időzítettnél az idő kötelező. |
| **Folyamat neve** | Kötelező, egyedi. |
| **Hányszor futhat maximum** | Az adott esemény hatására hányszor futhat le a folyamat összesen (pl. "csak 15 kupont osztok ki" → 15). |
| **Esemény típusa** | Legördülő; ez határozza meg az elérhető szabályokat és cseremezőket. |
| **Eseményhez tartozó szabályok** | `Hozzáad`-dal új szabálysor. Szabályok közt **ÉS**, egy szabályon belül az értékek közt **VAGY**. Pl. „összes eddigi rendelés összege ≤ 1 500 000 Ft ÉS irányítószám 9400 vagy 9700". |
| **Művelet** | Email küldése / Webhook / Vásárló áthelyezése vásárló csoportba. |

### Elévülés (fontos!)

Időzített folyamatoknál bizonyos esemény-párok között **elévülés** él: két
azonos esemény közül mindig csak az **utolsó** számít, illetve egy "lezáró"
esemény törli a függőben lévő műveletet. Ezért nem kap a vásárló annyi levelet,
ahányszor a kosárba tett valamit.

Értelmezett párok:
- `kosár elhagyás → kosár elhagyás` (csak az utolsó kosárállapot számít)
- `kosár elhagyás → megrendelés leadás` (ha megrendel, a függő levél **nem megy ki**)
- `hírlevél feliratkozás → hírlevél leiratkozás`
- `regisztráció / adatmódosítás → vásárló törlése`

### Műveletek

#### Email küldése
- Ki kell választani egy **hírlevél sablont** (`Marketing / Hírlevél / Hírlevél
  sablonok`). A rendszer ezt küldi az esemény hatására annak a felhasználónak,
  akire a szabályok igazak.
- Perc pontos időzítés. Címzettkör szűkíthető a szabályokkal. Dedikált címzettnek
  (pl. admin) is küldhető — pl. „szólj emailben, ha nagy értékű rendelés jött".
- **Kosárelhagyás email**nél feltételként adható: kosárban lévő tételek **száma,
  neve, ára**.

#### Webhook
- Az esemény adatait `HTTP POST` küldi a megadott URL-re, **JSON** törzzsel.
- Max 2 perc futásidő.
- Hitelesíthető HMAC-kulccsal (`Beállítások / Külső kapcsolatok / API kapcsolat`
  → Webhook igazolása), MITM ellen.

#### Vásárló áthelyezése vásárló csoportba
- Pl. ha az összköltés elér egy szintet → átkerül „VIP" csoportba, és onnantól
  élvezi annak minden beállítását (kedvezmény, ár, stb.).

### Tipikus receptek

| Cél | Esemény | Időzítés | Szabály | Művelet |
|---|---|---|---|---|
| Elhagyott kosár 1. emlékeztető | kosár elhagyás | +1 óra | feliratkozott hírlevélre = igen | Email (emlékeztető sablon) |
| Elhagyott kosár 2. (ösztönző) | kosár elhagyás | +48 óra | feliratkozó = igen; csoport ≠ viszonteladó | Email (kupon sablon) |
| Welcome levél | vásárló regisztráció | +10 perc | — | Email (welcome sablon) |
| Nagy rendelés riasztás adminnak | megrendelés leadás | azonnal | végösszeg ≥ X | Email dedikált címre |
| Törzsvásárlóvá léptetés | megrendelés leadás | azonnal | összköltés ≥ X | Csoportba helyezés |
| Külső rendszer értesítése | megrendelés leadás | azonnal | — | Webhook |

### Cseremezők

A sablonokban használható cseremezők az `ertesitesek-cseremezok.md` fájlban
vannak felsorolva, a "melyik eseménynél érhető el" megkötésekkel együtt.
Kosár-eseménynél elérhető pl. `[product_list]`, `[product_table]`,
`[product_table_quantity]`; rendelés-eseménynél `[order_key]`, `[url_payment]`,
`[order_authlink]`, `[package_number]` stb.


---


# 3. Elhagyott kosár visszaszerzése

### Elhagyott kosár visszaszerzése — playbook

**Hivatalos oldalak:**
- https://unas.hu/tudastar/admin/elhagyott-kosarak
- https://unas.hu/tudastar/admin/automata-folyamatok
- https://unas.hu/tudastar/admin/koveto-hirlevel

### 1. Mit tud az Unas

| | Követő hírlevél | **Automata folyamatok** (ajánlott) |
|---|---|---|
| Menü | `Marketing / Hírlevél / Követő hírlevél` | `Beállítások / Automata folyamatok` |
| Legkorábbi küldés | **1 nap** | **~5 perc**, perc pontossággal |
| Feltételek | vásárló csoport, "Új vásárló", "Feliratkozott hírlevélre", "Kereső kifejezés" (kosár termékneveiben), termékszűrés | ugyanezek + kosár tételszám / név / ár, összköltés, irányítószám, stb. |
| Sorozat | több sablon, de mind napos lépcső | 1 folyamat = 1 levél; több folyamat = sorozat |
| Elágazás megnyitás/kattintás alapján | nincs | nincs (csak idő-alapú + "rendelt → leáll") |

#### Kötelező előfeltételek
- **Szerverre mentett kosár** bekapcsolva: `Beállítások / Alapbeállítások / Működés`.
- **Ismert e-mail cím**: a levél csak akkor megy ki, ha a látogató bejelentkezett
  vásárló, vagy a pénztár első lépésében megadta az e-mailjét.
- Az `Elhagyott kosarak` lista (`Megrendelések` főmenü alatt) mutatja: kosárelhagyás
  dátuma, vásárló e-mail, név, tételszám. Kosarak 1 évig tárolva. Exportálható.

### 2. Ajánlott logika (idő-alapú, 2–3 lépcső)

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

### 3. Beállítási checklist

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

### 4. GDPR

- Az elhagyott kosár e-mail Magyarországon **direkt marketingnek** minősül →
  biztonságos: csak marketing/hírlevél hozzájárulást adott címzettnek küldj.
  Ezért van minden folyamaton a "Feliratkozott hírlevélre = igen" feltétel.
- Minden levél alján `[link_unsubscribe]`.
- "Jogos érdek" alapon nem-feliratkozóknak küldeni szürke zóna — csak adatvédelmi
  szakértő jóváhagyásával.

### 5. Sablonvázak (kiindulás, testre szabandó)

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


---


# 4. Marketing: hírlevél, SMS, push, intelligens tartalom

### Marketing: hírlevél, feliratkozók, SMS/push, intelligens tartalom, partnerprogram, vélemények

**Főmenü:** `Marketing`
Kapcsolódó: `references/automata-folyamatok.md`, `references/kedvezmenyek.md`,
`references/ertesitesek-cseremezok.md`

### Hírlevél

**Hivatalos:** https://unas.hu/tudastar/admin/hirlevel

#### Sablon szerkesztés — `Marketing / Hírlevél / Hírlevél sablonok`
- `Létrehoz` → tárgy + törzs, WYSIWYG szerkesztő. Ugyanezek a sablonok
  használhatók egyszeri levélként és automata folyamat / követő hírlevél
  műveleteként is.
- Cseremezők a tárgyban és törzsben: `[name]`, `[email]`, `[cust_id]`,
  `[username]`, `[points_account]`, `[points_account_raw]`, `[discount_sum]`,
  `[discount_direct]`, `[address]`, `[date]`, `[link_unsubscribe]`.
  Rendeléshez kötött követő levélben továbbá: `[order_key]`, `[order_amount]`,
  `[order_date]`, `[points_credited]`, `[shipping_address]`, `[url_track]`,
  `[url_payment]`.
  Kosárelhagyás követő levélben: `[product_list]`, `[product_table]`,
  `[product_list_opinion]`, `[product_table_opinion]`.
- Többnyelvű bolt: nyelvenként külön sablon.

#### Hírlevél küldés — `Marketing / Hírlevél / Hírlevél küldés`
- Kiválasztott sablon egyszeri kiküldése. Szűrés: nyelv, célközönség (összes
  regisztrált / hírlevelet igénylők / külön feliratkozók), **vásárló csoport**,
  megrendelés státusz, "van összeg a pontgyűjtő számlán".
- Feladó név + feladó e-mail kötelező kiküldés előtt.
- Előnézet: kiküldhető csak az admin kapcsolattartónak.
- **Keret:** STANDARD-ban a terméklimittel megegyező, PREMIUM/VIP-ben a
  terméklimit kétszerese db hírlevél/hó. E fölött 0,1 Ft+ÁFA/db. Aktuális
  egyenleg a menüben látszik; `Egyenleg feltöltése` gomb.

#### Követő hírlevél — `Marketing / Hírlevél / Követő hírlevél`
**Hivatalos:** https://unas.hu/tudastar/admin/koveto-hirlevel
- Esemény után **min. 1 nap** késleltetéssel automata levél. Rövidebb időhöz →
  automata folyamatok.
- Követés típusa: megrendelés után, rendelés-státuszváltásra, hírlevél
  feliratkozás után, regisztráció után, **kosár elhagyás** (speciális; szerverre
  mentett kosár kell).
- Feltételek: "Új vásárló", vásárló csoport (a napok leteltekor ellenőrzi a
  csoporttagságot), megrendelés státusz, "Feliratkozott hírlevélre", "Van összeg
  a pont egyenlegen", "Volt kuponfelhasználás a rendelésben", **Kereső kifejezés**
  (a rendelés/kosár termékneveiben, vesszős lista = VAGY), **Szűrés termékek
  alapján** (adott termék a kosárban/rendelésben, VAGY kapcsolat).
- "A címzett maximum hányszor kaphatja meg ezt a hírlevelet".
- Klasszikus használat: 1 év múlva "cseréld a fogyóeszközt" újravásárlási
  emlékeztető adott termékre szűrve.

#### Feliratkozók — `Marketing / Hírlevél / Feliratkozók listája`
- Regisztrált vásárló is igényelhet hírlevelet, és regisztráció nélkül is lehet
  feliratkozni. Szűrés csoport / dátum / típus szerint. Feliratkozó
  adatbázis külön almenü (export/import).
- **Mindig tartsd be a hírlevél-jogszabályokat** (opt-in, leiratkozás).

#### Külső hírlevélküldő — `Marketing / Hírlevél / Külső hírlevélküldő`
- Számos hazai/nemzetközi ESP integrálva (pl. Mailchimp, Klaviyo-szerű
  megoldások, hazai szolgáltatók). Előbb náluk kell regisztrálni/előfizetni,
  utána az onnan kapott adatokat kell itt beállítani.

### SMS — `Marketing / SMS`
- Sablonok, direkt SMS egy vásárlónak, egyenleg. SMS-hez egyenlegfeltöltés kell
  (`Marketing / SMS / SMS / Hírlevél egyenleg feltöltés`). Tipikus: csomag
  feladva / átadva a futárnak értesítés — a rendelés-státuszokhoz köthető
  (`references/megrendelesek.md`).

### Push üzenetek — `Marketing / Push üzenetek`
- Webes push notification. Előfeltétel: **webalkalmazás (PWA) bekapcsolva**
  (`Beállítások / Webalkalmazás (PWA)`). Sablonok + küldés almenük. Magas
  megnyitási arány, gyors célba érés.

### Intelligens tartalom — `Marketing / Intelligens tartalom`
**Hivatalos:** https://unas.hu/tudastar/admin/intelligens-tartalom
- Felugró / beúszó ablak vagy szkript, **feltételrendszerrel**: új vs. régi
  vásárló, van-e termék a kosárban, hány oldalt nézett, mennyi ideje van az
  oldalon, vásárló csoport, időzítés.
- Megjelenés: hagyományos felugró / beúszó (Triton, Oberon, Nova-szerű
  kinézeteknél, jobbról-balról-alulról-felülről) / szkript (az intelligens
  tartalom feltételrendszerével futtatott kód — jobb, mint a sima szkript
  beszúrás).
- Tartalom típus: hírlevél feliratkozás, hírlevél feliratkozás kuponajánlattal,
  kép+link, videó+link, szerencsekerék, szerencsekerék hírlevél feliratkozással.

### Partnerprogram (affiliate) — `Marketing / Partnerprogram`
**Hivatalos:** https://unas.hu/tudastar/admin/partnerprogram
- Partneronként: fix vagy százalékos jutalék (max. jutalék megadható), egyedi
  **kupon kód** (szóban átadott kódra is jár jutalék + a vevő kedvezményt kap),
  e-mail (a partner a saját vásárlói profiljában látja a rendeléseit/jutalékát),
  automata vagy kézi partner-kód, egyedi követő link (ikonra kattintva
  másolható).
- Beállítások fül: cookie élettartam (alapból **60 nap**), mely rendelés-státusz
  alapján számoljon jutalékot. Elszámolás dátumszűréssel, elég korábbra állítva,
  hogy a státusz már végleges legyen.

### Vélemények — `Marketing / Vélemény, Szavazás, Fórum / Vélemény`
**Hivatalos:** https://unas.hu/tudastar/admin/velemeny
- Csillagos értékelés + szöveg + előny/hátrány. Strukturált adatként beágyazva →
  csillagok a Google találati listán (SEO).
- Beállítások: beépített funkció vs. Facebook Comments; reCaptcha; e-mail cím
  kezelése; **adminisztrátori válasz**; "csak regisztrált és belépett vásárló
  írhat"; "csak igazolt vásárló írhat" (aki tényleg megvette); igazolt vélemény
  megjelölése.
- Kevesen térnek vissza véleményt írni — emlékeztesd őket **követő hírlevéllel**
  (`[product_table_opinion]` / `[product_list_opinion]` cseremező).


---


# 5. Kedvezmények, akciók, pontgyűjtés

### Kedvezmények, akciók, pontgyűjtés, utó- és csomagajánlat

**Főmenü:** `Marketing` (Kedvezmények szekció)
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/kedvezmenyek

Alapszabály: ha több kedvezmény típus is teljesül egy vásárlóra, jellemzően a
**nagyobb** érvényesül (nem összeadódik) — kivéve, ahol a leírás mást mond
(pl. vásárló csoport közvetlen + végösszeg kedvezmény együtt hat).

### Kuponok, ajándékkártyák — `Marketing / Kuponok, ajándékkártyák`
**Hivatalos:** https://unas.hu/tudastar/admin/kuponok-ajandekkartyak
- **Végösszeg kedvezmény kupon:** összegszerű vagy százalékos; érvényességi idő;
  minimum vásárlási összeg. Százaléknál az alap a termékek eladási ára +
  esetleges közvetlen termékkedvezmény.
- **Termék kedvezmény kupon:** konkrét termékekre / kategóriákra.
- **Ingyenes szállítás kupon** is generálható.
- Beállítható: hányszor használható fel, meddig érvényes, összeghatár.
- Terjesztés: hírlevélben, nyomtatva, offline.

### Ajándéktermékek — `Marketing / Ajándéktermékek`
**Hivatalos:** https://unas.hu/tudastar/admin/ajandektermekek
- `Ajándéktermék használata` kapcsoló. Szabályonként: megnevezés, **kosárérték**
  küszöb (bruttó), kosárérték-számítás alapja (teljes kosár VAGY csak az
  "Ezekhez adható ajándék" termékek értéke — utóbbi márkaspecifikus akcióhoz).
- Az ajándék a rendelésben külön 0 értékű tételként jelenik meg (raktár- és
  számlabarát). Több ajándékakció futhat párhuzamosan; a rendszer a kosár
  alapján mutatja a választható ajándékokat.
- Ha van kosárérték-küszöb, az ajándékválasztás csak a kosár oldalon jelenik meg,
  a termékadatlapon nem.

### Mennyiségfüggő akciók — `Marketing / Mennyiségfüggő akciók`
**Hivatalos:** https://unas.hu/tudastar/admin/mennyisegfuggo-akciok
- "1-et fizet 2-t kap" és minden variánsa. A jogosító és az ajándék/kedvezményes
  termék lehet különböző. Mezők: megnevezés, érvényességi idő, kedvezmény
  mértéke, rendelésenkénti felhasználás max., "Ki veheti igénybe?" (regisztrált /
  új / hírlevél-feliratkozó), vásárló csoport, "Ezekhez használható fel"
  (termékek/kategóriák + min. darab), "Ezekből választható" (termékek/kategóriák
  + darab).

### Időszakos árváltozás — `Marketing / Időszakos árváltozás`
**Hivatalos:** https://unas.hu/tudastar/admin/idoszakos-arvaltozas
- Előre ütemezett akciók/áremelések (Black Friday, hétvégi akció, ünnep).
  Mezők: megnevezés, **publikus időszak**, **megjelenés periódusa** (ismétlődő,
  napra/hónapra/hét napjára, óra-percre, nyitvatartás és munkaszüneti napok
  figyelembevételével), mérték (%), **irány** (negatív = akció, pozitív =
  áremelés), árszámítás alapja (normál vagy egyedi akciós ár), vásárló csoport.
- **Figyelem:** időszakos árcsökkentés NEM teszi a terméket a "speciális akciós"
  kategóriába, és nem vált ki árcsökkenés-értesítőt.

### Kosárérték kedvezmény — `Marketing / Kosárérték kedvezmény`
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

### Pontgyűjtés — `Marketing / Pontgyűjtés`
**Hivatalos:** https://unas.hu/tudastar/admin/pontgyujtes
- 1 pont = 1 pénznemegység. Beállítható: pontgyűjtés ki/be, regisztrációért /
  hírlevél-megerősítésért járó pont, alap felhasználási beállítás
  ("Felhasználom" / "Nem"), akciós termékre jár-e pont (és %-os generálásnál),
  a végösszeg hány %-áig fedezhető pontból, alap pontérték a termék bruttó ára
  után, pont lejárat.
- Kombinálható a hírlevéllel: pont lejárata előtt emlékeztető ("van összeg a
  pont egyenlegen" feltétellel).

### Utóajánlat — `Marketing / Utóajánlat`
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

### Csomagajánlat — `Marketing / Csomagajánlat`
**Hivatalos:** https://unas.hu/tudastar/admin/csomagajanlat
- Együtt vásárolt termékekből dinamikus árú csomag a termékadatlapon (nem kell
  külön cikkszám, mint a csomagterméknél; a számlán külön tételek).
- `Használom a csomagajánlat funkciót` kapcsoló; max. hány ajánlat a
  termékadatlapon. Ajánlatonként: aktív, érvényességi idő, **árképzés típusa**
  (normál/akciós árból összegszerű vagy százalékos kedvezmény, vagy fix ár).

### Vásárló csoport kedvezmények
Lásd `references/vasarlok-csoportok.md` — közvetlen % a termékárból + végösszeg %
+ minimum rendelési összeg + kosárérték-kedvezmény tiltás/engedélyezés
csoportonként.


---


# 6. Rendszer-értesítők és cseremezők

### Rendszer-értesítők és cseremezők (merge fields)

### Értesítések — `Beállítások / Vásárlási folyamat / Értesítések`
**Hivatalos:** https://unas.hu/tudastar/admin/ertesitesek

- A webáruház sok eseménynél küld e-mailt vagy SMS-t (vásárlónak és/vagy
  adminnak). Itt aktiválható / kikapcsolható / szerkeszthető minden üzenet.
- Minden üzenettípusnál külön **Admin** és **Vásárló** oszlop jelöli, ki kapja.
- A feladó e-mail cím módosítható (`Módosít` az adott sorban).
- `[order_products]` a rendelés-értesítőben a tételeket adja — ne töröld.
- Beállítható: PDF csatolmány a rendelés-e-mailekhez; normál vs. nyomtatóbarát
  (kép nélküli) admin-e-mail kinézet; termékképek a rendelés-értesítőkben.
- SMS-hez egyenleg kell: `Marketing / SMS / SMS / Hírlevél egyenleg feltöltés`.
- Rendelés-**státuszváltáskor** külön státusz-értesítő küldhető
  (e-mail és/vagy SMS) — a státusznál állítható be, hogy automatikus legyen
  (`references/megrendelesek.md`).

### Cseremezők — teljes lista

A szögletes zárójeles kódok a levél tárgyában és törzsében a kiküldéskor a
konkrét adatra cserélődnek. **Csak akkor működnek, ha az adott eseménynél van
hozzájuk adat** (lásd a megkötéseket a végén).

#### Kapcsolattartó / vásárló
| Cseremező | Tartalom |
|---|---|
| `[name]` | kapcsolattartó neve |
| `[email]` | kapcsolattartó e-mail címe |
| `[username]` | felhasználónév (e-mailes azonosításnál az e-mail) |
| `[cust_id]` | felhasználó egyedi azonosítója |
| `[address]` | összefűzött cím (ir.szám, város, utca, házszám) |
| `[cust_contact]` | kapcsolati adatok táblázatban |
| `[cust_invoice-shipping]` / `[cust_billing-shipping]` | számlázási + szállítási adatok táblázatban |
| `[cust_shipping]` | szállítási adatok táblázatban |
| `[cust_other]` | egyéb adatok (vásárló paraméterek) |
| `[discount_sum]` | végösszeg-kedvezmény %-a (mindig lekérdezve) |
| `[discount_direct]` | közvetlen termékkedvezmény %-a (mindig lekérdezve) |
| `[total_ordered_amount]` | a vásárló összköltése |
| `[date]` | aktuális dátum |

#### Pontgyűjtés
`[points_account]` (pl. „2000 Ft"), `[points_account_raw]` (pl. „2000"),
`[points_credited]` (utolsó rendeléshez felírt pont).

#### Hírlevél
`[link_subscribe]` (feliratkozás-megerősítő link), `[link_unsubscribe]`
(leiratkozó link — DM levélben kötelező).

#### Rendelés
| Cseremező | Tartalom |
|---|---|
| `[order_key]` | rendelés száma |
| `[order_amount]` / `[order_total]` | rendelés végösszege |
| `[order_date]` | rendelés dátuma |
| `[order_comment]` | rendeléshez fűzött megjegyzés |
| `[shipping_comment]` | szállító felé megadott megjegyzés |
| `[order_status]` / `[order_status_text]` | státusz / státusz szövege |
| `[order_data]` | egyéb rendelés adatok (megrendelés paraméterek) |
| `[order_auth]` / `[order_authlink]` | rendelés-megerősítő kattintható link |
| `[shipping_method]` / `[shipping_method_det]` | szállítási mód / leírása |
| `[payment_method]` / `[payment_method_det]` | fizetési mód / leírása |
| `[shipping_address]` / `[billing_address]` | szállítási / számlázási cím |
| `[package_number]` | csomagszám |
| `[url_track]` | rendeléskövetés oldal (regisztrált és vendég vásárlónak is) |
| `[url_payment]` | azonnali fizetés indítása belépés nélkül |
| `[old_payment_method_name]` / `[new_payment_method_name]` | fizetésimód-váltásnál a régi/új mód neve |

#### Számla (csak „Megrendelés státusz váltás" eseménynél)
`[invoice_num]`, `[invoice_pdf_url]` / `[invoice_link]`.

#### Termékek (rendelés-leadás és elhagyott kosár eseménynél)
| Cseremező | Tartalom |
|---|---|
| `[product_list]` | kosárba/rendelésbe tett termékek listája |
| `[product_table]` | `[product_list]` + termék fő képe |
| `[product_table_quantity]` | `[product_list]` + mennyiség |
| `[product_list_opinion]` | terméklista, ahol az URL a véleményezéshez visz |
| `[product_table_opinion]` | ua. + fő kép |

#### Bolt
`[shop_data]` — az áruház adatai táblázatban.

### Megkötések
- A `[product_*]` mezők csak ott, ahol van termékadat (rendelés leadás,
  elhagyott kosár).
- Rendelés-specifikus mezők (`[package_number]` stb.): "megrendelés leadás" és
  "megrendelés státusz váltás" eseménynél.
- Vásárlóhoz kötött mezők: csak ha az esemény bekövetkeztekor van adat a
  vásárlóról. Kivétel `[discount_direct]`, `[discount_sum]` — mindig lekérve.
- "Vásárló törlés" és "vásárló adatmódosítás" eseménynél csak `[email]` áll
  rendelkezésre.


---


# 7. Megrendelések

### Megrendelések: lista, részletek, státuszok, csomagfeladás, visszáru, számlázás, összeszedés, export

**Főmenü:** `Megrendelések`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/megrendelesek

### Megrendelések listája
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

### Megrendelés részletek
**Hivatalos:** https://unas.hu/tudastar/admin/megrendeles-reszletek
- Gombok: Vissza, Nyomtat, Szállítólevél, Elállási nyilatkozat, **Másolás**
  (rendelés duplikálása), **Számlázás** (ha Számlázható státuszú),
  **Újrakalkulál** (szállítási + kezelési költség újraszámítása módosítás után),
  Töröl.
- Három blokk: alapadatok (azonosító, leadás/módosítás ideje, státusz, típus,
  számlázás állapota), tételek, vásárlói/címadatok.
- `Státusz értesítő` gomb: e-mail a vásárlónak státuszváltáskor.

### Megrendelés státuszok, típusok
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

### Csomagfeladás / futár
**Hivatalos:** https://unas.hu/tudastar/admin/csomagfeladas
- Kétféle integráció: **fájl alapú** (letöltesz egy fájlt, feltöltöd a futár
  szoftverébe) és **API** (teljesen automata: egy gombbal átadod a rendelést,
  visszajön a **csomagszám**, letölthető a címke; a csomagszám státusz-értesítővel
  továbbküldhető a vevőnek).
- Kezeli az átvételi pontot, csomagautomatát, postán maradót, cserecsomagot.
- Integrálás: szerződés a futárral → `Beállítások / Fizetés, Szállítás,
  Logisztika / Speciális szállítási módok`.
- Napi teendő: `Megrendelések / Csomagfeladás` — szállító cégenként `Letölt`.

### Visszáru kezelés
**Hivatalos:** https://unas.hu/tudastar/admin/visszaru-kezeles
- Bekapcsoláskor létrejön két *Visszáru* típusú státusz (Visszaküldés alatt /
  Visszaküldve); kikapcsoláskor törlődnek.
- Beállítható: alap státusz admin által / vásárló által indított
  visszaküldéshez; milyen státuszba váltáskor generálódjon **visszatérítéses
  kupon** (kell: kuponkezelés bekapcsolva); milyen státuszba váltáskor vonja
  vissza a **pontokat** (kell: pontgyűjtés bekapcsolva).
- "A vásárló indíthat visszaküldést" külön kapcsoló.

### Számlázás, ügyvitel
**Hivatalos:** https://unas.hu/tudastar/admin/szamlazas-ugyvitel
- 40+ számlázóprogram; egy részéhez Unas fejlesztette a kapcsolatot
  (aktiválási díj, Unas support), másokat a szoftvergyártó (külső fejlesztés,
  ott a support). API-n gyakorlatilag bármelyik bekötehető.
- Folyamat: vagy a számlázóprogram kéri le a számlázható rendeléseket, vagy az
  adminból indítod (egyesével a rendelés részletekből, vagy tömegesen).

### Összeszedés
**Hivatalos:** https://unas.hu/tudastar/admin/osszeszedes
- Raktári komissiózó lista. Kell hozzá 4 megrendelés-státusz (Összeszedhető /
  Összeszedés folyamatban / Részben összeszedett / Összeszedve) és egy
  termék-paraméter a tárhelynek. Lista max. rendelésszám + max. tételszám +
  szállítási mód szerint.

### Megrendelések exportálása
**Hivatalos:** https://unas.hu/tudastar/admin/megrendelesek-exportalasa
- Excel export; szűrés fizetési/szállítási mód, vásárló csoport, státusz,
  dátum szerint. Választható: 1 sor = 1 rendelés, vagy 1 sor = 1 rendelés-tétel.

### Beszerzés
`Megrendelések / Beszerzés` — a rendelésekhez szükséges, de hiányzó készlet
alapján beszerzési javaslat/lista a beszállítók felé.


---


# 8. Termékek és készlet

### Termékek, kategóriák, paraméterek, tömeges módosítás, raktárkezelés, feed import

**Főmenü:** `Termékek`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/termekek

### Kategóriák
**Hivatalos:** https://unas.hu/tudastar/admin/kategoriak-letrehozasa
**Menü:** `Termékek / Kategóriák kezelése`
- Tetszőleges mélységű fa. **Kategóriák száma max. a csomag terméklimitjének
  fele.** Sorrend: ABC vagy kézi (`Beállítások / Alapbeállítások / Kategória`).
- Ugyanitt hozol létre terméket egy kategórián belül (`Új termék`).
- Speciális kategóriák (újdonságok, akciós termékek) külön kezelve.

### Termékek létrehozása
**Hivatalos:** https://unas.hu/tudastar/admin/termekek-letrehozasa
- `Termékek / Kategóriák kezelése` → kategória → `Új termék`. Lapfülek:
  alapadatok, képek, paraméterek, SEO, kapcsolódó/kiegészítő termékek, stb.
- **Cikkszám = azonosító**; `Ment új termékként` csak más cikkszámmal.
- Mentés-variánsok: `Ment majd raktár`, `Ment és marad`, `Ment`.

### Termék paraméterek
**Hivatalos:** https://unas.hu/tudastar/admin/termek-parameterek
**Menü:** `Beállítások / Termék beállítások / Termék paraméterek`
- Típusok: szabad szavas; szabad szavas többértékű (TAG, vesszős, szűrésnél
  ÉS/VAGY); **értékkészlet** (fix lista, elgépelés-védett — a tömeges feltöltésnél
  fontos); értékkészlet többértékű; szám; (továbbá kép, link, dátum stb.).
- **Figyelem:** értékkészlet típusban a gyorskereső nem keres.
- Használat: összehasonlítás, szűrés-box, ár-összehasonlító feed speciális
  mezői (Gyártó, ISBN, Szállítási idő…).

### Termék státuszok
**Hivatalos:** https://unas.hu/tudastar/admin/termek-statuszok
- Max. 3 egyéb státusz (pl. Előrendelhető, Outlet, Kiemelt). Szűrhető a
  kategóriában, ha engedélyezed: `Beállítások / Alapbeállítások / Működés` →
  szűrés-box beállítás. Többnyelvűnél nyelvenként.

### Csoportos módosítás
**Hivatalos:** https://unas.hu/tudastar/admin/csoportos-modositas
- Egy kategória összes termékének **ugyanazon** paraméterét ugyanazzal az
  értékkel/aránnyal módosítja (pl. nettó ár +5%, ÁFA-kulcs csere). Először példát
  mutat egy terméken, aztán végrehajt. Főkategória választása = minden benne
  lévő termék.

### Listás módosítás
**Hivatalos:** https://unas.hu/tudastar/admin/listas-modositas
- Leszűrt listában **egyenként eltérő** értékek írhatók: ár, készlet, státusz,
  tömeg. Lista-módok: egy kategóriában lévő / kép nélküli / keresés eredménye /
  véleménnyel rendelkező / raktárkezelésben kezelt-nem kezelt / készlethiányos.
- Változatok készletét itt NEM lehet — `Termékek / Kategóriák kezelése`.

### Raktárkezelés
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

### Automata import, feed bekötés
**Hivatalos:** https://unas.hu/tudastar/admin/automata-termek-import
- Külső adatforrásból (pl. nagykereskedelmi feed) napi/heti termék- és
  ár-frissítés, új termék felvitel, képek. **Egyedi fejlesztés** (formátum-
  konverziós modul) + üzemeltetési díj (terméklimit + gyakoriság függvénye).
  Az Unas előzetesen egyeztet az igényről.
- Alternatíva saját integrációra: `setProduct` / `setProductDB` API
  (`references/api.md`).

### Termék adatbázis export/import
`Termékek / Termék adatbázis` — teljes termékkör Excel/CSV export és
visszatöltés; fizetési/szállítási mód tiltás, vásárló csoport láthatóság az
"Azonosító a Webáruházban" mezőkkel hivatkozva.


---


# 9. Vásárlók és vásárló csoportok

### Vásárlók és vásárló csoportok

**Menü:** `Megrendelések / Vásárlók`
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlok-kezelese

### Vásárlók listája / adatlap
- `Vásárlók listája`: regisztrált vásárlók, szűrés csoport / dátum / típus
  szerint. Adatlapon: kapcsolattartó, számlázási + szállítási cím, adószám,
  ÁFA-mentesség, vásárló típus (Magánszemély / Cég / Egyéb), paraméterek,
  hírlevél státusz, pont egyenleg, kedvezmények, rendelések.
- Új vásárló kézzel is felvehető; kedvezmény egyénileg is adható (a csoport
  mellett).

### Vásárló csoportok — a legfontosabb szegmentáló eszköz
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlo-csoportok
**Menü:** `Megrendelések / Vásárlók / Vásárló csoportok`

Csoportonként beállítható:
| Mező | Hatás |
|---|---|
| **Azonosító a Webáruházban** | export/importban erre hivatkozol (mely csoport veheti meg a terméket) |
| **Csoport neve** | pl. Nagykereskedő, VIP, PRO, Klub, Versenyző |
| **Vásárló felületen választható** | a vevő önmagát is besorolhatja (pl. „belépés nagykereskedőként") |
| **Megrendelés végösszegből adott kedvezmény (%)** | a termékár nem változik, a végösszegből vonódik; a sávos végösszeg-kedvezménnyel nem adódik össze (a nagyobb érvényesül) |
| **Közvetlenül a termék árából adott kedvezmény (%)** | belépés után minden terméknél csökkentett ár látszik |
| **Minimum rendelési összeg** | a csoport tagjának ekkora rendelés alatt nem enged leadni |

- Ha csoportnál **közvetlen ÉS végösszeg** kedvezmény is be van állítva, **mindkettő
  érvényesül**.
- A vásárlóhoz egyénileg és a csoporthoz beállított azonos típusú kedvezmény
  közül a **nagyobb** érvényesül.
- **Kosárérték-alapú kedvezmény** csoportonként tiltható/engedélyezhető (pl.
  nagykernek ne járjon) — lásd `references/kedvezmenyek.md`.
- Csoportonként külön: hírlevél/követő hírlevél célzás, automata folyamat
  feltétel, mennyiségfüggő akció, időszakos árváltozás, utóajánlat.
- **Vendég / nem bejelentkezett vásárlónak nincs csoportja** — a legtöbb
  elhagyott kosár ilyen; ők az "alap" (csoport nélküli) ágba esnek.

### Vásárló export / import
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlo-adatbazis
**Menü:** `Megrendelések / Vásárlók / Vásárló adatbázis`
- Export: választható mezők, csak hírlevél-igénylők, csoport-szűrés, tömörítés.
- Import: e-mail (vagy beállítástól függően felhasználónév) alapján azonosít.
  Max 5 MB (fölötte ZIP). Tömeges csoportba sorolás / kedvezmény ezzel.
- Kulcs mezők: `E-mail`, `Kap. Név/Telefon/Mobil`, `Száll. */Szám. *` cím,
  `Adószám`, `ÁFA mentesen vásárolhat`, `Vásárló típus`, `Paraméter`,
  `Hírlevél` (igen/nem), pont mezők.

### Vásárló paraméterek
`Beállítások / Vásárlási folyamat / Vásárló paraméterek` — egyedi mezők a
vásárlóhoz (pl. „klubtagság", „szerződésszám"), amikre automata folyamat és
hírlevél is szűrhet.


---


# 10. Alapbeállítások és vásárlási folyamat

### Alapbeállítások, vásárlási folyamat, fizetés/szállítás, nyelvek, jog/GDPR

**Főmenü:** `Beállítások`

### Alapbeállítások
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

### Vásárlási folyamat
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlasi-folyamat
**Menü:** `Beállítások / Vásárlási folyamat` — almenük: megrendelés
státuszok/típusok, megrendelés paraméterek, vásárló paraméterek, értesítések
(`references/ertesitesek-cseremezok.md`), visszáru, e-mail-ellenőrzés,
cím-ellenőrzés, gyorsrendelés, megrendelés törlés.
- **Hírlevél-feliratkozó jelölőnégyzet a pénztárban** itt / az Alapbeállításokban
  kapcsolható be. **Alapból ne legyen bepipálva** (előre bepipált = jogsértő).

### Fizetési módok
**Hivatalos:** https://unas.hu/tudastar/admin/fizetesi-modok
**Menü:** `Beállítások / Fizetés, Szállítás, Logisztika / Fizetési módok`
- Alap: Készpénzzel a helyszínen / Előre utalással / Utánvéttel. `Hozzáad` újhoz.
- Mezők: `Azonosító a Webáruházban` (export/importhoz), megnevezés, leírás,
  **alternatív leírás** (az értesítő e-mailekben ez jelenik meg, ha ki van
  töltve), típus (átutalás / készpénz / utánvét / csekk / egyéb), kezelési
  költség, aktív.
- Online kártya / részletfizetés: `Bankkártyás, speciális fizetési módok`
  almenü (Barion, SimplePay, OTP, PayPal, áruhitel stb.).

### Szállítási módok
**Hivatalos:** https://unas.hu/tudastar/admin/szallitasi-modok
- `Hozzáad`; `Azonosító a Webáruházban`, megnevezés, leírás, alternatív leírás
  (értesítőben), nyelvenkénti szövegek, aktív kapcsoló, szállítási költség.
- **Speciális szállítási módok** almenü: futár API-k / fájl integrációk
  (`references/megrendelesek.md` — csomagfeladás).
- Kapcsolódó: szállítási költségek, szállítási területek, átvételi pontok,
  országok kezelése, kiszervezett logisztika (3PL/fulfilment).

### Szállítás és fizetés kapcsolás
**Hivatalos:** https://unas.hu/tudastar/admin/szallitas-es-fizetes-kapcsolas
- Fizetési módonként korlátozható, mely szállítási mód választható (pl.
  „Készpénz a helyszínen" → csak „Személyes átvétel"). Fizetési módonként min. 1
  szállítási mód kell.

### Pénznemek, árkijelzés
**Hivatalos:** https://unas.hu/tudastar/admin/penznemek-arkijelzes
- Több pénznem, ÁFA-beállítások, árformátum (kerekítés, kijelzés).

### Nyelvek beállítása
**Hivatalos:** https://unas.hu/tudastar/admin/nyelvek-beallitasa
**Menü:** `Beállítások / Szövegek, Nyelvek / Nyelvek beállítása`
- Alapnyelv + további nyelvek; nyelvenként pénznem. Hiányzó fordítások:
  `Beállítások / Szövegek, Nyelvek / Alapszövegek`. Nyelvenként külön domain
  kérhető (ügyfélszolgálat). Nyelv **törlése törli** a hozzá tartozó szövegeket.
- Külön ország több adminnal = külön Unas webáruház, nem nyelv.

### Jog / GDPR
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


---


# 11. SEO és tartalmi oldalak

### SEO, meta, robots.txt, llms.txt, URL-kezelés, tartalmi oldalak

**Főmenü:** `Marketing / Keresőoptimalizálás, SEO` és `Tartalom`
**Hivatalos gyűjtő:** https://unas.hu/tudastar/admin/keresooptimalizalas-seo

### SEO beállítások
**Hivatalos:** https://unas.hu/tudastar/admin/seo-beallitasok
**Menü:** `Marketing / Keresőoptimalizálás, SEO / SEO beállítások`
- Közös META adatok hozzáfűzése az egyénileg megadott / automatikusan generált
  meta adatokhoz (külön kapcsolók).
- META title max. hossz (optimum **60**), description max. (optimum **160**),
  keywords alapból **0** (a Google nem használja → nem kerül a forráskódba).
- **Robots META tag** alapérték: `index/noindex`, `follow/nofollow` — kategória-,
  termék-, plusz oldal szinten felülírható.
- Referrer-policy META tag.

### Egyéb SEO almenük
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

### Vélemények és SEO
A termékvélemények strukturált adatként (csillag) beágyazódnak → gazdagabb
Google találat. Lásd `references/marketing-hirlevel.md` (Vélemények).

### Tartalom / plusz oldalak
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

### Kinézet / arculat
`Beállítások / Kinézet, arculat` — kinézet választás/testreszabás, egyedi
kinézet, box-sorrend, arculati elemek, **szkript beszúrás**
(`script-beszuras` — fej/láb kód; feltételes futtatáshoz inkább intelligens
tartalom szkript típus), mobil változat. Fejlesztői részletek:
`references/api.md` (JS API) és https://unas.hu/tudastar/design


---


# 12. Külső kapcsolatok: API, Facebook, Google, piacterek

### Külső kapcsolatok: API, Facebook, Google, piacterek, feed, statisztika

**Főmenü:** `Beállítások / Külső kapcsolatok` és `Statisztika, Napló, Elemzés`

### API kapcsolat
**Hivatalos:** https://unas.hu/tudastar/admin/api-kapcsolat
**Menü:** `Beállítások / Külső kapcsolatok / API kapcsolat`
- **API kulcs alapú azonosítás** (ajánlott): `API kulcs létrehozása` →
  megnevezés, engedélyezett API funkciók kiválasztása, engedélyezett IP-k /
  tartományok (CIDR; üres = mind).
- Felhasználónév alapú azonosítás: csak régi integrációknak, újhoz **ne**.
- **Webhook igazolása:** HMAC kulcs generálás/törlés — MITM ellen a webhook
  hívások hitelesítésére.
- Részletes végpontlista és adatszerkezetek: `references/api.md`.

### Facebook kapcsolatok
**Hivatalos:** https://unas.hu/tudastar/admin/facebook-kapcsolatok
- **Facebook pixel**: a FB Vállalkozáskezelőben generált kód beillesztése;
  nyelvenkénti kód. Követett események: PageView, ViewContent, Search,
  AddToCart, InitiateCheckout, AddPaymentInfo, Lead, CompleteRegistration,
  Purchase, AddToWishlist. Külön vásárlásra és hírlevél-feliratkozásra.
- **Konverziók API (CAPI)**: szerver-oldali eseményküldés (iOS14 óta kell). A FB
  Eseménykezelőben generált hozzáférési kód + a domain beállítása.
- Több pixel: ügyfélszolgálat.

### Google kapcsolatok
**Hivatalos:** https://unas.hu/tudastar/admin/google-kapcsolatok
- **Google Analytics** (GA4 „G-" és régi „UA-" kód; több kód ENTER-rel;
  nyelvenként). Másnap már látszik az adat.
- **Google Ads** konverziókövetés: konverció kód + név a köszönőoldalhoz;
  vásárlásra és hírlevél-feliratkozásra. **Kibővített konverziók** kapcsoló a
  pontosabb méréshez.
- Google Merchant / Shopping feed: az árösszehasonlító feednél (lent).

### Piacterek
**Hivatalos:** https://unas.hu/tudastar/admin/piacterek
- Integrációk: UnasPlaza, Árukereső Marketplace, eMAG Marketplace, Allegro,
  Wolt. Termékek szinkronizálása a piactérre; részletes leírás
  piacterenként az adminban.

### Árösszehasonlító export, Feed
**Hivatalos:** https://unas.hu/tudastar/admin/arosszehasonlito-export-feed
- Automata export bekapcsolása → az egyes szolgáltatók (Árukereső, Google
  Shopping, Facebook, stb.) a saját formátumukban kérhetik le a termék-feedet a
  megjelenő URL-eken. Max. **napi 10 lekérés / formátum**, csak a szolgáltató
  IP-iről. „Ügynökségi IP" mezővel a hirdetéskezelő ügynökség is hozzáfér.
- Speciális mezők (Gyártó, Garancia, Szállítási idő, ISBN…) plusz adat /
  paraméter formájában (`references/termekek-keszlet.md`).

### Egyéb külső kapcsolatok
- **Külső marketing rendszerek** (`kulso-marketing-rendszerek`): hőtérkép /
  session-replay, prediktív kereső, push, marketing-automatizáló platformok.
- **Külső hírlevélküldő** (`kulso-hirlevelkuldo`): lásd
  `references/marketing-hirlevel.md`.
- **Minősítő rendszerek** (`minosito-rendszerek`): Árukereső Megbízható Bolt,
  Google Vásárlói értékelés stb.
- **Közösségi média** (`kozossegi-media`), **Chat a látogatóval**
  (`chat-a-latogatoval`).
- **Webáruházak szinkronizálása** (`webaruhazak-szinkronizalasa`): több Unas
  bolt közti termék/rendelés szinkron.

### Statisztika, Napló, Elemzés
**Hivatalos:** https://unas.hu/tudastar/admin/statisztika-naplo-elemzes
- **Látogatási statisztika**, **Termék statisztika**, **Megrendelés statisztika**
  (`megrendeles-statisztika`): rendelésszám, tétel/termékszám, nettó/bruttó,
  szállítási díj, kezelési költség, kedvezmények (összeg + %), pontfelhasználás,
  kuponhasználat; grafikon fizetési/szállítási mód, vásárló csoport, terület
  szerint. **A sikertelen státuszú rendelések nincsenek benne.**
- **Termék feliratkozások** (értesíts, ha raktáron lesz).
- Naplók: admin-napló, háttérfolyamat-napló, vásárló-napló, API-napló.


---


# 13. Unas XML API, webhook, JS API

### Unas XML API + webhook + JavaScript API

**Hivatalos:** https://unas.hu/tudastar/api
**Admin oldali kulcskezelés:** `references/kulso-kapcsolatok.md`

### Alapok

- **XML alapú REST-szerű API.** Nem nyelvfüggő. Lehetőség: lekérdezés,
  módosítás, új adat rögzítése, törlés — akár kétirányú szinkron külső
  rendszerekkel (számlázó, készlet, ERP, marketing).
- Végpont-minta: `getX` (olvasás) és `setX` (írás) párok.
- **Azonosítás** (https://unas.hu/tudastar/api/azonositas):
  1. Admin: `Beállítások / Külső kapcsolatok / API kapcsolat` → API kulcs
     létrehozása, funkció-scope és IP-korlát megadása.
  2. `login` hívás az API kulccsal → **token**, ami **2 órán át** él. Minden
     további hívás ezzel a tokennel.
  - A felhasználónév+jelszó mód elavult, új integrációhoz tilos.
- **Limitek** (https://unas.hu/tudastar/api/limitaciok):
  - Óradíj IP-nként: **PREMIUM 2000 hívás/óra, VIP 6000 hívás/óra**.
  - Sikertelen hívás max. 20/végpont (egy sikeres nullázza a számlálót);
    külön: 5 sikertelen azonosítás/óra.
  - Limitsértés → **1 óra IP-tiltás** az adott boltra; azonosíthatatlan
    kérésözön → 2 óra teljes API-csend.
  - `set` XML max. **128 MB**.
  - Éjfél ±10 perc: karbantartás, ne indíts hívást. Nagy napi hívásokat
    véletlen időpontra ütemezz.

### Végpontok (getX / setX + Adatszerkezet + Példák aloldalak)

| Erőforrás | Végpontok | Megjegyzés |
|---|---|---|
| Megrendelések | `getOrder`, `setOrder` | rendelés le/feltöltés, státuszváltás |
| Raktárkészlet | `getStock`, `setStock` | készlet szinkron |
| Termékek | `getProduct`, `setProduct`, `getProductDB`, `setProductDB` | egyedi ill. teljes adatbázis |
| Termék paraméterek | `getProductParameter`, `setProductParameter` | |
| Kategóriák | `getCategory`, `setCategory` | |
| Vásárlók | `getCustomer`, `setCustomer`, `checkCustomer` | |
| Vásárló csoportok | `getCustomerGroup`, `setCustomerGroup` | |
| Hírlevél feliratkozók | `getNewsletter`, `setNewsletter` | ESP-szinkron |
| Scriptek | `getScriptTag`, `setScriptTag` | fej/láb kód injektálás |
| Plusz menük/oldalak | `getPage`, `setPage` | |
| Tartalmi elemek | `getPageContent`, `setPageContent` | |
| Fájlok/mappák | `getStorage`, `setStorage` | |
| **Automata folyamatok** | `getAutomatism`, `setAutomatism`, webhook-ellenőrzés | |
| Megrendelés státuszok | `getOrderStatus`, `setOrderStatus` | |
| Megrendelés típusok | `getOrderType`, `setOrderType` | |
| Kuponok | `getCoupon`, `setCoupon` | egyedi kuponkód-generálás |
| Fizetési/szállítási módok | `getMethod`, `setMethod` | |
| További raktárak | `getWarehouse`, `setWarehouse` | |
| Átvételi pontok / pont-csoportok | `getDeliveryPoint(Group)`, `setDeliveryPoint(Group)` | |
| Csomagajánlatok | `getPackageOffer`, `setPackageOffer` | |
| Termék vélemények | `getProductReview`, `setProductReview` | |
| Beállítások | `getSetting`, `setSetting` | ÁFA, jogi dok., pénznem adatszerkezetek |
| Termék plusz szolgáltatások | `getProductService`, `setProductService` | |
| Termék matricák | `getSticker`, `setSticker` | |
| Ajándéktermék szabályok | `getGift`, `setGift` | |
| Mennyiségfüggő akciók | `getBogo`, `setBogo` | |

Minden erőforrásnál van `Adatszerkezet` és `Példák` aloldal a tudástárban:
`https://unas.hu/tudastar/api/<eroforras>-adatszerkezet` és `-peldak`.

### Webhook (automata folyamatok művelete)
- `HTTP POST`, JSON törzs az esemény adataival. Max 2 perc futásidő.
- Hitelesítés: HMAC kulcs (`API kapcsolat / Webhook igazolása`), ellenőrzés
  leírása: https://unas.hu/tudastar/api/automata-folyamatok-webhook-ellenorzes

### JavaScript API (frontend)
**Hivatalos:** https://unas.hu/tudastar/design/js-api
- A vásárlói felületen **csak olvasás** (product, last order, cart, belépett
  vásárló). Írás/módosítás/törlés nincs.
- Aszinkron, JSON válasz. A node-nevek a normál API XML node-jaiból `_`
  tagolással: `SumPriceGross` → `sum_price_gross`.
- Csak akkor használd, ha a sablonban nem áll rendelkezésre az adat.
- Almenük: `js-api-cart`, `js-api-order`, `js-api-product`, `js-api-customer`,
  `js-api-shop` (mind `-request` / `-response`).

### Kinézet / sablon fejlesztés
**Hivatalos:** https://unas.hu/tudastar/design — sablon alapelemei, boxok,
oldaltartalmak, beágyazott elemek, `main.cfg` (`beallitasok-valtozok`,
`back-end-valtozok`), stíluslapok, **sablonszerkesztő** (blokk-átrendezés,
`layout_config` a `main.cfg`-ben; csak termléklista / termékrészletek / főoldal).


---
