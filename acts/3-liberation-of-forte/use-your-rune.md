# Use Your Rune

> Your rune is a rune like any other.

Once it has a Phantasm, Ledger walks the same paths as Whisper or Keeper: Sentinel inserts it, the runite awakens it, the Grimoire reads it, the footer counts it.

## Insert
```bash
php cast sentinel --runite-insert=Ledger
```
Sentinel writes the two lines at the markers:
```php
use Rune\Ledger\Manifest as Ledger;
#sentinel-manifest
// …
Ledger::ether()::essence()::entity();
#sentinel-awaken
```
`--runite-remove=Ledger` takes them out again.

## Read it in the Grimoire
```bash
php cast grimoire --runic=Ledger
```
```
 #  L E D G E R —— 0.2
Keeps a small ledger of income and expense in one flow.

  [M] Rune\Ledger\Manifest
  [O] …/@liberation/Ledger
  [U] Anwar

  ::L I N K
    Weaver entity 1.7
    Aether entity 1.17

  ::N O D E
    ether
    LEDGER_CURRENCY
      The currency written before every amount.
    …
```
The header warns *Carefull use rune BETA/DEPRECATED* — your rune is BETA until you mark it `EXIST`. (DEPRECATED in that header is not a mark anymore.)

## It counts
- `aether_list_runes()` now ends with `Ledger`.
- The footer `Version=` includes Ledger's version.
- The main hall still shows the same casts — a rune adds powers, not casts. Casts come from your runite.

## Remove
```bash
php cast sentinel --runic-delete=Ledger
```
Deletes `@liberation/Ledger/` and removes it from the runite. Only liberation runes can be removed; origin runes stay.

## From your rune to Rune
A liberation rune is private until you share it. Two ways out:
- **With an app** — it travels as shards inside a relic ([Share It](share-it.md)).
- **To Rune itself** — when it proves its purpose, it can be proposed as a new origin rune ([Contributing](../4-the-beyond/contributing.md)).
