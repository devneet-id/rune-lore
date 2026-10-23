# A New Runite

> Engrave an app from nothing — no template.

<!-- status: draft · sources: runites/README.md (skeleton), rune-cookbook.md, scratch runite wallet · tested in rune-dev/scenario (scratch) -->

Awakening gave you a runite from an artefact. Now you start from an empty file, the way the built-in runites were made. We engrave **wallet**: a ledger that remembers — Ledger counts, Keeper keeps.

## 1 · Plan before you engrave
Write what the app does as casts and spells:

| Cast | Spells | Does |
|---|---|---|
| `add` | `--amount`, `--note` | add one entry and keep it |
| `book` | — | show every entry and the total |

Then choose the runes — **only** the ones the casts need: Aether, Whisper, Weaver, Chanter (always) · Keeper (memory; it needs Forger and Cipher) · Ledger (our rune).

## 2 · The empty file
A file named `wallet`, no `.php`, so it starts with the shebang ([the cast file](../0-the-void/the-cast-file.md)):
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::liberation();
```
Write the [skeleton](../../runites/README.md) by hand — `use`, `#sentinel-manifest`, awaken, `#sentinel-awaken`, begin, `#sentinel-codex`, end — or write only the four runes and let Sentinel add the rest:
```bash
php wallet sentinel --invoke=Keeper
php wallet sentinel --invoke=Ledger
```
(Then add `Keeper::begin()` / `Keeper::end()` yourself.)

## 3 · The whole runite
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::liberation();

use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
use Rune\Forger\Manifest as Forger;
use Rune\Cipher\Manifest as Cipher;
use Rune\Keeper\Manifest as Keeper;
use Rune\Ledger\Manifest as Ledger;
#sentinel-manifest
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
Forger::ether()::essence()::entity();
Cipher::ether()::essence()::entity();
Keeper::ether()::essence()::entity();
Ledger::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();
Chanter::begin();
Keeper::begin();


// Ledger lives in one flow; Keeper carries its entries to the next
function wallet_load() {
  foreach ((array) Keeper::item('entries') as $entry) {
    Ledger::add($entry->amount, $entry->note);
  }
}

function wallet_save() {
  global $LEDGER_ENTRIES;
  Keeper::item('entries', $LEDGER_ENTRIES);
}


Chanter::cast('add --amount --note', function() {
  $amount = (float) Chanter::spell('amount');
  if (!$amount) {
    Whisper::echo("{{color-warning}}{{icon-warning}} Give an amount: --amount=-50000{{nl}}");
    return;
  }
  wallet_load();
  $count = Ledger::add($amount, (string) (Chanter::spell('note') ?: ''));
  wallet_save();
  Whisper::echo("{{color-success}}{{icon-success}} entry #$count kept{{nl}}");
}, 'Add an entry. --amount=-50000 --note=coffee');

Chanter::cast('book', function() {
  wallet_load();
  foreach (Ledger::lines() as $line) Whisper::echo("$line{{nl}}");
  Whisper::echo("{{color-success}}= " . LEDGER_CURRENCY . ' ' . number_format(Ledger::total()) . "{{nl}}");
}, 'Show the whole book.');


#sentinel-codex
Chanter::end();
Keeper::end();
Aether::end();
```
```
$ php wallet add --amount=5000000 --note=salary
[√] entry #1 kept
$ php wallet add --amount=-50000 --note=coffee
[√] entry #2 kept
$ php wallet book
+ IDR 5,000,000  salary
- IDR 50,000  coffee
= IDR 4,950,000
```
On Linux and macOS, `chmod +x wallet` and run `./wallet book` — the shebang finds PHP.

## What to notice
- **Runes do not know each other's memory.** Ledger lives in one flow; the runite glues it to Keeper (`wallet_load`, `wallet_save`). That glue belongs in the runite, not inside Ledger — one rune, one purpose.
- **Small helpers are fine in a runite.** Prefix them with the runite's name (`wallet_*`) so they never meet a rune's names.
- **The main screen is your help page.** The third argument of every `Chanter::cast()` is what users read.

Next: [Many Runites](many-runites.md).
