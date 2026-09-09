# Unas XML API + webhook + JavaScript API

**Hivatalos:** https://unas.hu/tudastar/api
**Admin oldali kulcskezelés:** `references/kulso-kapcsolatok.md`

## Alapok

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

## Végpontok (getX / setX + Adatszerkezet + Példák aloldalak)

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

## Webhook (automata folyamatok művelete)
- `HTTP POST`, JSON törzs az esemény adataival. Max 2 perc futásidő.
- Hitelesítés: HMAC kulcs (`API kapcsolat / Webhook igazolása`), ellenőrzés
  leírása: https://unas.hu/tudastar/api/automata-folyamatok-webhook-ellenorzes

## JavaScript API (frontend)
**Hivatalos:** https://unas.hu/tudastar/design/js-api
- A vásárlói felületen **csak olvasás** (product, last order, cart, belépett
  vásárló). Írás/módosítás/törlés nincs.
- Aszinkron, JSON válasz. A node-nevek a normál API XML node-jaiból `_`
  tagolással: `SumPriceGross` → `sum_price_gross`.
- Csak akkor használd, ha a sablonban nem áll rendelkezésre az adat.
- Almenük: `js-api-cart`, `js-api-order`, `js-api-product`, `js-api-customer`,
  `js-api-shop` (mind `-request` / `-response`).

## Kinézet / sablon fejlesztés
**Hivatalos:** https://unas.hu/tudastar/design — sablon alapelemei, boxok,
oldaltartalmak, beágyazott elemek, `main.cfg` (`beallitasok-valtozok`,
`back-end-valtozok`), stíluslapok, **sablonszerkesztő** (blokk-átrendezés,
`layout_config` a `main.cfg`-ben; csak termléklista / termékrészletek / főoldal).
