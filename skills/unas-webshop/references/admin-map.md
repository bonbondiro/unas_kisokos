# Unas tudástár — teljes témakör-térkép

Minden téma egy sora: **slug — egymondatos leírás**. A hivatalos oldal:
`https://unas.hu/tudastar/admin/<slug>` (kivéve ahol más prefix van jelölve).
Ha részlet kell (mezők, limitek), kérd le a megfelelő URL-t (`fetch()` /
`WebFetch` — az `<article>` szerver-oldalon renderelt).

A mélyebb, saját szavas jegyzetek a testvér-fájlokban vannak — a "→" mutatja,
melyikben.

---

## Megrendelések (főmenü)

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

### Megrendelések / Vásárlók → `vasarlok-csoportok.md`
`vasarlok-kezelese`, `vasarlok-listaja`, `vasarlo-adatlap`, `vasarlo-adatbazis`
(export/import), `vasarlo-csoportok`.

---

## Termékek (főmenü) → `termekek-keszlet.md`

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

### Termékek / Raktárkezelés
`raktarkezeles`, `raktarkeszlet-statisztika`, `raktarkeszlet-adatbazis`,
`raktarcimkek`, `tovabbi-raktarak`, `raktarkeszlet-intervallumok`
(készlet-sáv szöveg), `beszallitok`, `felveteli-helyek`,
`automata-termek-import` (feed, egyedi fejlesztés).

---

## Marketing (főmenü)

### Hírlevél, SMS, push → `marketing-hirlevel.md`
`hirlevel`, `hirlevel-szerkesztes` (sablon + cseremezők), `hirlevel-kuldes`
(keret, célközönség), `koveto-hirlevel` (min. 1 nap, kosárelhagyás is),
`feliratkozok-listaja`, `feliratkozo-adatbazis`, `kulso-hirlevelkuldo`,
`sms` / `sms-sablonok` / `sms-kuldes` / `sms-hirlevel-egyenleg(-feltoltes)`,
`push-uzenetek` / `push-sablonok` / `push-kuldes`, `intelligens-tartalom`
(felugró/beúszó, feltételrendszer), `partnerprogram` (affiliate).

### Kedvezmények → `kedvezmenyek.md`
`kedvezmenyek`, `kuponok-ajandekkartyak`, `ajandektermekek`,
`mennyisegfuggo-akciok`, `idoszakos-arvaltozas`, `kosarertek-kedvezmeny`,
`pontgyujtes`, `utoajanlat`, `csomagajanlat`.

### Egyéb marketing
| slug | leírás |
|---|---|
| `marketing` | marketing gyűjtő oldala |
| `hirek-naptar` | blog/hír modul + eseménynaptár |
| `kulso-marketing-rendszerek` | hőtérkép, session replay, prediktív kereső, automatizáló platformok |
| `nyomtathato-arlista` | PDF árlista generálás |
| `velemeny-szavazas-forum` / `velemeny` / `szavazas` / `forum` | termékvélemény (csillag, SEO), szavazás, fórum modul |
| `partnerprogram` | affiliate (fent is) |

### Keresőoptimalizálás, SEO → `seo-tartalom.md`
`keresooptimalizalas-seo`, `seo-beallitasok`, `automatikus-sef-es-meta-generalas`,
`kozos-meta-adatok`, `egyeni-meta-adatok`, `url-kezeles`, `robots-txt-kezeles`,
`llms-txt-kezeles`.

---

## Tartalom (főmenü) → `seo-tartalom.md`
`tartalom`, `plusz-menuk-oldalak`, `tartalmi-elem-kezeles`, `banner-boxok`,
`szerkesztheto-tartalmak`, `tarolt-urlapok`, `fajlkezelo`.

---

## Statisztika, Napló, Elemzés (főmenü) → `kulso-kapcsolatok.md`
`statisztika-naplo-elemzes`, `latogatasi-statisztika`, `termek-statisztika`,
`termek-feliratkozasok`, `megrendeles-statisztika`, `admin-naplo`,
`hatterfolyamat-naplo`, `vasarlo-naplo`, `api-naplo`, `kulso-statisztikak`.

---

## Beállítások (főmenü)

### Alapbeállítások → `beallitasok-vasarlas.md`
`beallitasok`, `alapbeallitasok` (lapfülek: Kategória / Termék / Vásárló /
Megrendelés / **Működés** [szerverre mentett kosár!] / Megjelenés / Marketing).

### Pénznemek, Árkijelzés
`penznemek-arkijelzes`, `penznemek`, `afa-beallitasok`, `arkijelzes`.

### Szövegek, Nyelvek
`szovegek-nyelvek`, `nyelvek-beallitasa`, `alap-szovegek`.

### Kinézet, arculat (→ részletek: `https://unas.hu/tudastar/design`)
`kinezet-arculat`, `kinezet-kivalasztasa`, `kinezet-testreszabasa`,
`egyedi-kinezet`, `oldal-kinezetek`, `modosithato-elemek`,
`ajanlok-top-termekek`, `box-sorrend-modositas`, `arculati-elemek`,
`script-beszuras`, `mobil-valtozat`.

### Fizetés, Szállítás, Logisztika → `beallitasok-vasarlas.md`, `megrendelesek.md`
`fizetes-szallitas-logisztika`, `fizetesi-modok`,
`bankkartyas-specialis-fizetesi-modok` (Barion, SimplePay, OTP, PayPal,
áruhitel), `szallitasi-modok`, `specialis-szallitasi-modok` (futár API-k),
`szallitasi-koltsegek`, `szallitas-es-fizetes-kapcsolas`,
`szallitasi-teruletek-kezelese`, `atveteli-pontok-kezelese`,
`orszagok-kezelese`, `kiszervezett-logisztika` (3PL/fulfilment).

### Termék beállítások → `termekek-keszlet.md`
`termek-beallitasok`, `termek-parameterek`, `termek-plusz-adatok`,
`termek-statuszok`, `plusz-szolgaltatasok`, `matricak`, `keresesi-beallitasok`.

### Vásárlási feltételek (jog) → `beallitasok-vasarlas.md`
`vasarlasi-feltetelek`, `altalanos-szerzodesi-feltetelek`,
`adatkezelesi-tajekoztato`, `kulso-aszf-megoldasok`, `adatkezelesi-beallitasok`
(cookie, GDPR, profilalkotás), `vasarlasi-tudnivalok`, `elallasi-nyilatkozat`.

### Vásárlási folyamat → `megrendelesek.md`, `ertesitesek-cseremezok.md`
`vasarlasi-folyamat`, `megrendeles-statuszok-tipusok`, `megrendeles-parameterek`,
`megrendeles-torles`, `gyorsrendeles`, `vasarlo-parameterek`, `ertesitesek`
(rendszer-e-mailek + cseremezők), `visszaru-kezeles`, `email-ellenorzes`,
`cim-ellenorzes`, `cimkek`.

### Automata folyamatok → `automata-folyamatok.md`
`automata-folyamatok` (esemény → feltétel → művelet, perc pontos, webhook).

### Külső kapcsolatok → `kulso-kapcsolatok.md`, `api.md`
`kulso-kapcsolatok`, `api-kapcsolat` (API kulcs, HMAC), `facebook-kapcsolatok`
(pixel + CAPI), `google-kapcsolatok` (GA4, Ads), `kozossegi-media`,
`piacterek` (+ `-unasplaza`, `-arukereso-marketplace`, `-emag-marketplace`,
`-allegro`, `-wolt`), `arosszehasonlito-export-feed`, `chat-a-latogatoval`,
`minosito-rendszerek`.

### Egyéb beállítások
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

## Más tudástár szekciók (nem `/admin/` prefix)

| Szekció | URL prefix | Tartalom |
|---|---|---|
| API dokumentáció | `https://unas.hu/tudastar/api/...` | XML API: azonosítás, limitációk, végpontok (`get*`/`set*`), adatszerkezetek, példák, webhook-ellenőrzés → `api.md` |
| Kinézet dokumentáció | `https://unas.hu/tudastar/design/...` | sablon alapelemei, boxok, oldaltartalmak, beágyazott elemek, `main.cfg` változók, stíluslapok, JS API, sablonszerkesztő |
| Ügyfélfiók | `https://unas.hu/tudastar/ugyfelfiok/...` | pénzügyek, szolgáltatások, domain, felhasználók, előfizető, partnerprogram (ügyfélfiók szint) |
| Integráció (fejlesztőknek) | `https://unas.hu/tudastar/integracio/...` | alkalmazás-integráció: első lépések, telepítés, törlés, demó |
| Hosting / Webtárhely | `https://unas.hu/tudastar/hosting/...` | domain, DNS, aldomain, SSL, e-mail fiók/továbbító/szűrés, FTP, MySQL/phpMyAdmin, ütemezett feladatok, naplók |
| Rendelés (előfizetés) | `https://unas.hu/tudastar/rendeles/...` | tesztáruház nyitás, webáruház-előfizetés, domain/webtárhely rendelés |
