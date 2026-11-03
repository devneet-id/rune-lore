# Runites

> A **runite** is a file you engrave with runes — by default named `cast`. Rune ships with a few runites of its own, kept in `@runite/`. They are the tools every runite can call.

**Engraving** is the act of writing a runite: you `use` runes, awaken them, and register **casts** with Chanter.

| Built-in runite | Called with | What it does | Needs |
|---|---|---|---|
| [Awakening](awakening.md) | `Rune\Ethereal::awakening()` | turns an empty `cast` into a runite: a blank template, or a relic of `devneet-id/reliquary` | — |
| [Rune](rune.md) | `php cast` | the main hall: stats, echoes, every cast with its note | Act 0 runes |
| [Grimoire](grimoire.md) | `php cast grimoire` | reads the runes (Phantasm) and the arcane | Act 0 runes (arcane: Keeper) |
| [Reliquary](reliquary.md) | `php cast reliquary` | seals a runite into a relic (`.rune`), opens relics, reads the reliquaries online | Act 0 runes (echoes & shards: Keeper) |
| [Sentinel](sentinel.md) | `php cast sentinel` | unlocks the modes, inserts / removes runes in your runite, liberation tools | Act 0 runes |

`Chanter::begin()` loads every built-in runite of `@runite/` except Awakening, so they appear under **DEFAULT** on the main hall (`rune` itself is hidden — it *is* the main hall). Your own casts appear under **REGISTERED**.

Every main hall speaks plain system words: one thing (`--runic`, `--shard`, `--relic`), a list (`--runic-list`, `--shards`, `--relics`), an action (`--runic-create`, `--shard-remove`), and a move from one to another (`--runite-relic`, `--relic-runite`). An old spell answers with its new name (*`--invoke` is now `--runite-insert`*).

## Modes
A runite can unlock modes. Each one is a line under the `require` line, written by Sentinel, and a folder next to the runite with a `README.md`:

| Mode | Unlock | Line | Folder | Caption |
|---|---|---|---|---|
| — | — | — | — | *The Awakening of Void* |
| Liberation | `sentinel --liberation` | `Rune\Ethereal::liberation();` | `@liberation/` — runes of your own | *The Liberation of Forte* |
| Federation | `sentinel --federation` | `Rune\Ethereal::federation();` | `@federation/` — your reliquary and its relics | *The Federation of Fides* |

Both modes can be open at once; the caption of the higher Act wins. A mode folder belongs to your project and goes into git.

## The shape of a runite
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
#sentinel-manifest
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();
Chanter::begin();

// your casts
Chanter::cast('hello', fn() => Whisper::echo('Hello, Rune!{{nl}}'), 'Say hello.');

#sentinel-codex
Chanter::end();
Aether::end();
```
- **Shebang** on line 1 when the file has no `.php` extension.
- The three markers `#sentinel-manifest`, `#sentinel-awaken`, `#sentinel-codex` are where Sentinel writes. Keep them.
- Every runite keeps its memory in `.echoes/<runite>/` next to itself (when Keeper is engraved), wherever it is cast from.
- A required spell is written in the cast `arg`, an optional one in its `echo`: `Chanter::cast(arg: 'reliquary --relic', echo: 'Inspect one relic (--tag=<version>)', …)`.
