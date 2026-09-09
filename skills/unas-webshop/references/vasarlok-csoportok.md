# Vásárlók és vásárló csoportok

**Menü:** `Megrendelések / Vásárlók`
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlok-kezelese

## Vásárlók listája / adatlap
- `Vásárlók listája`: regisztrált vásárlók, szűrés csoport / dátum / típus
  szerint. Adatlapon: kapcsolattartó, számlázási + szállítási cím, adószám,
  ÁFA-mentesség, vásárló típus (Magánszemély / Cég / Egyéb), paraméterek,
  hírlevél státusz, pont egyenleg, kedvezmények, rendelések.
- Új vásárló kézzel is felvehető; kedvezmény egyénileg is adható (a csoport
  mellett).

## Vásárló csoportok — a legfontosabb szegmentáló eszköz
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

## Vásárló export / import
**Hivatalos:** https://unas.hu/tudastar/admin/vasarlo-adatbazis
**Menü:** `Megrendelések / Vásárlók / Vásárló adatbázis`
- Export: választható mezők, csak hírlevél-igénylők, csoport-szűrés, tömörítés.
- Import: e-mail (vagy beállítástól függően felhasználónév) alapján azonosít.
  Max 5 MB (fölötte ZIP). Tömeges csoportba sorolás / kedvezmény ezzel.
- Kulcs mezők: `E-mail`, `Kap. Név/Telefon/Mobil`, `Száll. */Szám. *` cím,
  `Adószám`, `ÁFA mentesen vásárolhat`, `Vásárló típus`, `Paraméter`,
  `Hírlevél` (igen/nem), pont mezők.

## Vásárló paraméterek
`Beállítások / Vásárlási folyamat / Vásárló paraméterek` — egyedi mezők a
vásárlóhoz (pl. „klubtagság", „szerződésszám"), amikre automata folyamat és
hírlevél is szűrhet.
