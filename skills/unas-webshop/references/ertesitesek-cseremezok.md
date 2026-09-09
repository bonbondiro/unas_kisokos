# Rendszer-értesítők és cseremezők (merge fields)

## Értesítések — `Beállítások / Vásárlási folyamat / Értesítések`
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

## Cseremezők — teljes lista

A szögletes zárójeles kódok a levél tárgyában és törzsében a kiküldéskor a
konkrét adatra cserélődnek. **Csak akkor működnek, ha az adott eseménynél van
hozzájuk adat** (lásd a megkötéseket a végén).

### Kapcsolattartó / vásárló
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

### Pontgyűjtés
`[points_account]` (pl. „2000 Ft"), `[points_account_raw]` (pl. „2000"),
`[points_credited]` (utolsó rendeléshez felírt pont).

### Hírlevél
`[link_subscribe]` (feliratkozás-megerősítő link), `[link_unsubscribe]`
(leiratkozó link — DM levélben kötelező).

### Rendelés
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

### Számla (csak „Megrendelés státusz váltás" eseménynél)
`[invoice_num]`, `[invoice_pdf_url]` / `[invoice_link]`.

### Termékek (rendelés-leadás és elhagyott kosár eseménynél)
| Cseremező | Tartalom |
|---|---|
| `[product_list]` | kosárba/rendelésbe tett termékek listája |
| `[product_table]` | `[product_list]` + termék fő képe |
| `[product_table_quantity]` | `[product_list]` + mennyiség |
| `[product_list_opinion]` | terméklista, ahol az URL a véleményezéshez visz |
| `[product_table_opinion]` | ua. + fő kép |

### Bolt
`[shop_data]` — az áruház adatai táblázatban.

## Megkötések
- A `[product_*]` mezők csak ott, ahol van termékadat (rendelés leadás,
  elhagyott kosár).
- Rendelés-specifikus mezők (`[package_number]` stb.): "megrendelés leadás" és
  "megrendelés státusz váltás" eseménynél.
- Vásárlóhoz kötött mezők: csak ha az esemény bekövetkeztekor van adat a
  vásárlóról. Kivétel `[discount_direct]`, `[discount_sum]` — mindig lekérve.
- "Vásárló törlés" és "vásárló adatmódosítás" eseménynél csak `[email]` áll
  rendelkezésre.
