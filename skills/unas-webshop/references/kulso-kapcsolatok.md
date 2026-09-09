# Külső kapcsolatok: API, Facebook, Google, piacterek, feed, statisztika

**Főmenü:** `Beállítások / Külső kapcsolatok` és `Statisztika, Napló, Elemzés`

## API kapcsolat
**Hivatalos:** https://unas.hu/tudastar/admin/api-kapcsolat
**Menü:** `Beállítások / Külső kapcsolatok / API kapcsolat`
- **API kulcs alapú azonosítás** (ajánlott): `API kulcs létrehozása` →
  megnevezés, engedélyezett API funkciók kiválasztása, engedélyezett IP-k /
  tartományok (CIDR; üres = mind).
- Felhasználónév alapú azonosítás: csak régi integrációknak, újhoz **ne**.
- **Webhook igazolása:** HMAC kulcs generálás/törlés — MITM ellen a webhook
  hívások hitelesítésére.
- Részletes végpontlista és adatszerkezetek: `references/api.md`.

## Facebook kapcsolatok
**Hivatalos:** https://unas.hu/tudastar/admin/facebook-kapcsolatok
- **Facebook pixel**: a FB Vállalkozáskezelőben generált kód beillesztése;
  nyelvenkénti kód. Követett események: PageView, ViewContent, Search,
  AddToCart, InitiateCheckout, AddPaymentInfo, Lead, CompleteRegistration,
  Purchase, AddToWishlist. Külön vásárlásra és hírlevél-feliratkozásra.
- **Konverziók API (CAPI)**: szerver-oldali eseményküldés (iOS14 óta kell). A FB
  Eseménykezelőben generált hozzáférési kód + a domain beállítása.
- Több pixel: ügyfélszolgálat.

## Google kapcsolatok
**Hivatalos:** https://unas.hu/tudastar/admin/google-kapcsolatok
- **Google Analytics** (GA4 „G-" és régi „UA-" kód; több kód ENTER-rel;
  nyelvenként). Másnap már látszik az adat.
- **Google Ads** konverziókövetés: konverció kód + név a köszönőoldalhoz;
  vásárlásra és hírlevél-feliratkozásra. **Kibővített konverziók** kapcsoló a
  pontosabb méréshez.
- Google Merchant / Shopping feed: az árösszehasonlító feednél (lent).

## Piacterek
**Hivatalos:** https://unas.hu/tudastar/admin/piacterek
- Integrációk: UnasPlaza, Árukereső Marketplace, eMAG Marketplace, Allegro,
  Wolt. Termékek szinkronizálása a piactérre; részletes leírás
  piacterenként az adminban.

## Árösszehasonlító export, Feed
**Hivatalos:** https://unas.hu/tudastar/admin/arosszehasonlito-export-feed
- Automata export bekapcsolása → az egyes szolgáltatók (Árukereső, Google
  Shopping, Facebook, stb.) a saját formátumukban kérhetik le a termék-feedet a
  megjelenő URL-eken. Max. **napi 10 lekérés / formátum**, csak a szolgáltató
  IP-iről. „Ügynökségi IP" mezővel a hirdetéskezelő ügynökség is hozzáfér.
- Speciális mezők (Gyártó, Garancia, Szállítási idő, ISBN…) plusz adat /
  paraméter formájában (`references/termekek-keszlet.md`).

## Egyéb külső kapcsolatok
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

## Statisztika, Napló, Elemzés
**Hivatalos:** https://unas.hu/tudastar/admin/statisztika-naplo-elemzes
- **Látogatási statisztika**, **Termék statisztika**, **Megrendelés statisztika**
  (`megrendeles-statisztika`): rendelésszám, tétel/termékszám, nettó/bruttó,
  szállítási díj, kezelési költség, kedvezmények (összeg + %), pontfelhasználás,
  kuponhasználat; grafikon fizetési/szállítási mód, vásárló csoport, terület
  szerint. **A sikertelen státuszú rendelések nincsenek benne.**
- **Termék feliratkozások** (értesíts, ha raktáron lesz).
- Naplók: admin-napló, háttérfolyamat-napló, vásárló-napló, API-napló.
