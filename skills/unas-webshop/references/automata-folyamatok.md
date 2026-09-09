# Automata folyamatok

**Menü:** `Beállítások / Automata folyamatok` → `Hozzáad`
**Hivatalos:** https://unas.hu/tudastar/admin/automata-folyamatok
**API-ból is kezelhető:** `getAutomatism` / `setAutomatism` (lásd `api.md`)

Esemény → (feltételek) → művelet. Ezzel váltható ki a legtöbb "ha X történik,
küldj levelet / hívj webhookot / sorold át a vásárlót" automatizmus. Erősebb és
gyorsabb, mint a *Követő hírlevél*.

## A folyamat mezői

| Mező | Jelentés |
|---|---|
| **Aktív** | Ki/be. Inaktívan az esemény nem vált ki műveletet. |
| **Időzített** | Ki: az esemény után azonnal (max ~5 perc). Be: megadható perc / óra / nap késleltetés az esemény után. Időzítettnél az idő kötelező. |
| **Folyamat neve** | Kötelező, egyedi. |
| **Hányszor futhat maximum** | Az adott esemény hatására hányszor futhat le a folyamat összesen (pl. "csak 15 kupont osztok ki" → 15). |
| **Esemény típusa** | Legördülő; ez határozza meg az elérhető szabályokat és cseremezőket. |
| **Eseményhez tartozó szabályok** | `Hozzáad`-dal új szabálysor. Szabályok közt **ÉS**, egy szabályon belül az értékek közt **VAGY**. Pl. „összes eddigi rendelés összege ≤ 1 500 000 Ft ÉS irányítószám 9400 vagy 9700". |
| **Művelet** | Email küldése / Webhook / Vásárló áthelyezése vásárló csoportba. |

## Elévülés (fontos!)

Időzített folyamatoknál bizonyos esemény-párok között **elévülés** él: két
azonos esemény közül mindig csak az **utolsó** számít, illetve egy "lezáró"
esemény törli a függőben lévő műveletet. Ezért nem kap a vásárló annyi levelet,
ahányszor a kosárba tett valamit.

Értelmezett párok:
- `kosár elhagyás → kosár elhagyás` (csak az utolsó kosárállapot számít)
- `kosár elhagyás → megrendelés leadás` (ha megrendel, a függő levél **nem megy ki**)
- `hírlevél feliratkozás → hírlevél leiratkozás`
- `regisztráció / adatmódosítás → vásárló törlése`

## Műveletek

### Email küldése
- Ki kell választani egy **hírlevél sablont** (`Marketing / Hírlevél / Hírlevél
  sablonok`). A rendszer ezt küldi az esemény hatására annak a felhasználónak,
  akire a szabályok igazak.
- Perc pontos időzítés. Címzettkör szűkíthető a szabályokkal. Dedikált címzettnek
  (pl. admin) is küldhető — pl. „szólj emailben, ha nagy értékű rendelés jött".
- **Kosárelhagyás email**nél feltételként adható: kosárban lévő tételek **száma,
  neve, ára**.

### Webhook
- Az esemény adatait `HTTP POST` küldi a megadott URL-re, **JSON** törzzsel.
- Max 2 perc futásidő.
- Hitelesíthető HMAC-kulccsal (`Beállítások / Külső kapcsolatok / API kapcsolat`
  → Webhook igazolása), MITM ellen.

### Vásárló áthelyezése vásárló csoportba
- Pl. ha az összköltés elér egy szintet → átkerül „VIP" csoportba, és onnantól
  élvezi annak minden beállítását (kedvezmény, ár, stb.).

## Tipikus receptek

| Cél | Esemény | Időzítés | Szabály | Művelet |
|---|---|---|---|---|
| Elhagyott kosár 1. emlékeztető | kosár elhagyás | +1 óra | feliratkozott hírlevélre = igen | Email (emlékeztető sablon) |
| Elhagyott kosár 2. (ösztönző) | kosár elhagyás | +48 óra | feliratkozó = igen; csoport ≠ viszonteladó | Email (kupon sablon) |
| Welcome levél | vásárló regisztráció | +10 perc | — | Email (welcome sablon) |
| Nagy rendelés riasztás adminnak | megrendelés leadás | azonnal | végösszeg ≥ X | Email dedikált címre |
| Törzsvásárlóvá léptetés | megrendelés leadás | azonnal | összköltés ≥ X | Csoportba helyezés |
| Külső rendszer értesítése | megrendelés leadás | azonnal | — | Webhook |

## Cseremezők

A sablonokban használható cseremezők az `ertesitesek-cseremezok.md` fájlban
vannak felsorolva, a "melyik eseménynél érhető el" megkötésekkel együtt.
Kosár-eseménynél elérhető pl. `[product_list]`, `[product_table]`,
`[product_table_quantity]`; rendelés-eseménynél `[order_key]`, `[url_payment]`,
`[order_authlink]`, `[package_number]` stb.
