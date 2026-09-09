# Marketing: hírlevél, feliratkozók, SMS/push, intelligens tartalom, partnerprogram, vélemények

**Főmenü:** `Marketing`
Kapcsolódó: `references/automata-folyamatok.md`, `references/kedvezmenyek.md`,
`references/ertesitesek-cseremezok.md`

## Hírlevél

**Hivatalos:** https://unas.hu/tudastar/admin/hirlevel

### Sablon szerkesztés — `Marketing / Hírlevél / Hírlevél sablonok`
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

### Hírlevél küldés — `Marketing / Hírlevél / Hírlevél küldés`
- Kiválasztott sablon egyszeri kiküldése. Szűrés: nyelv, célközönség (összes
  regisztrált / hírlevelet igénylők / külön feliratkozók), **vásárló csoport**,
  megrendelés státusz, "van összeg a pontgyűjtő számlán".
- Feladó név + feladó e-mail kötelező kiküldés előtt.
- Előnézet: kiküldhető csak az admin kapcsolattartónak.
- **Keret:** STANDARD-ban a terméklimittel megegyező, PREMIUM/VIP-ben a
  terméklimit kétszerese db hírlevél/hó. E fölött 0,1 Ft+ÁFA/db. Aktuális
  egyenleg a menüben látszik; `Egyenleg feltöltése` gomb.

### Követő hírlevél — `Marketing / Hírlevél / Követő hírlevél`
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

### Feliratkozók — `Marketing / Hírlevél / Feliratkozók listája`
- Regisztrált vásárló is igényelhet hírlevelet, és regisztráció nélkül is lehet
  feliratkozni. Szűrés csoport / dátum / típus szerint. Feliratkozó
  adatbázis külön almenü (export/import).
- **Mindig tartsd be a hírlevél-jogszabályokat** (opt-in, leiratkozás).

### Külső hírlevélküldő — `Marketing / Hírlevél / Külső hírlevélküldő`
- Számos hazai/nemzetközi ESP integrálva (pl. Mailchimp, Klaviyo-szerű
  megoldások, hazai szolgáltatók). Előbb náluk kell regisztrálni/előfizetni,
  utána az onnan kapott adatokat kell itt beállítani.

## SMS — `Marketing / SMS`
- Sablonok, direkt SMS egy vásárlónak, egyenleg. SMS-hez egyenlegfeltöltés kell
  (`Marketing / SMS / SMS / Hírlevél egyenleg feltöltés`). Tipikus: csomag
  feladva / átadva a futárnak értesítés — a rendelés-státuszokhoz köthető
  (`references/megrendelesek.md`).

## Push üzenetek — `Marketing / Push üzenetek`
- Webes push notification. Előfeltétel: **webalkalmazás (PWA) bekapcsolva**
  (`Beállítások / Webalkalmazás (PWA)`). Sablonok + küldés almenük. Magas
  megnyitási arány, gyors célba érés.

## Intelligens tartalom — `Marketing / Intelligens tartalom`
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

## Partnerprogram (affiliate) — `Marketing / Partnerprogram`
**Hivatalos:** https://unas.hu/tudastar/admin/partnerprogram
- Partneronként: fix vagy százalékos jutalék (max. jutalék megadható), egyedi
  **kupon kód** (szóban átadott kódra is jár jutalék + a vevő kedvezményt kap),
  e-mail (a partner a saját vásárlói profiljában látja a rendeléseit/jutalékát),
  automata vagy kézi partner-kód, egyedi követő link (ikonra kattintva
  másolható).
- Beállítások fül: cookie élettartam (alapból **60 nap**), mely rendelés-státusz
  alapján számoljon jutalékot. Elszámolás dátumszűréssel, elég korábbra állítva,
  hogy a státusz már végleges legyen.

## Vélemények — `Marketing / Vélemény, Szavazás, Fórum / Vélemény`
**Hivatalos:** https://unas.hu/tudastar/admin/velemeny
- Csillagos értékelés + szöveg + előny/hátrány. Strukturált adatként beágyazva →
  csillagok a Google találati listán (SEO).
- Beállítások: beépített funkció vs. Facebook Comments; reCaptcha; e-mail cím
  kezelése; **adminisztrátori válasz**; "csak regisztrált és belépett vásárló
  írhat"; "csak igazolt vásárló írhat" (aki tényleg megvette); igazolt vélemény
  megjelölése.
- Kevesen térnek vissza véleményt írni — emlékeztesd őket **követő hírlevéllel**
  (`[product_table_opinion]` / `[product_list_opinion]` cseremező).
