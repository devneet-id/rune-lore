# The Flow

> One run, from the first rune awakened to the last line of the footer.

<!-- status: draft · sources: Rune/Manifest.php, Aether/Manifest.php, Chanter/Manifest.php, Keeper/Manifest.php, runes/aether.md, runes/chanter.md, runes/keeper.md -->

A runite is read from top to bottom, once. Nothing runs by itself: runes are loaded, the flow is opened, casts are only *registered* — and the real work happens when the flow is closed.

## The whole run

```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';    // 1. Composer knows where Rune\ lives

use Rune\Aether\Manifest as Aether;               // 2. call the runes by their Manifest
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
use Rune\Forger\Manifest as Forger;
use Rune\Cipher\Manifest as Cipher;
use Rune\Keeper\Manifest as Keeper;
#sentinel-manifest
Aether::ether()::essence()::entity();             // 3. awaken: load the rune's files
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
Forger::ether()::essence()::entity();
Cipher::ether()::essence()::entity();
Keeper::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();                                  // 4. open the flow
Chanter::begin();
Keeper::begin();

Chanter::cast('hello --name', function() {        // 5. register (not run!)
  $name = Chanter::spell('name') ?: 'traveler';
  Whisper::echo(Weaver::bind('Hello, {{name}}.{{nl}}', ['name' => $name]));
  return $name;
}, 'Say hello.');

#sentinel-codex
Chanter::end();                                   // 6. run the cast asked on the command line
Keeper::end();                                    // 7. keep the arcane
Aether::end();                                    // 8. footer, then exit
```

```
$ php cast hello --name=Anwar
Hello, Anwar.

◇Version=1.12.31: ϟExecute=0.0049s, ΞMemory=1.07MB - ^1.26MB
```

## Step by step

| Step | What really happens |
|---|---|
| **Awaken** | `ether()`, `essence()` and `entity()` each `require_once` one file of the rune (`Ether.php`, `Essence.php`, `Entity.php`) and add the rune to a list Aether keeps. The order matters: Ether defines the constants that Essence and Entity use. |
| `Aether::begin()` | Cleans memory (`gc_collect_cycles`), empties the arcane, writes the first arcane line `Aether.manifest.begin`. |
| `Chanter::begin()` | Loads the built-in casts from `@bindrune/chanter/`: `artefact`, `grimoire`, `rune`, `sentinel`. |
| `Keeper::begin()` | Makes `.echoes/<runite>/` (with `arcanes/`, `shards/`, `arcane.txt`, `shard.json`), empties `glitch.txt`, and starts catching glitches. |
| `Chanter::cast(...)` | Stores the callable under its name and keeps its echo for the main screen. **Nothing runs yet.** |
| `Chanter::end()` | Reads the command line, finds the cast and runs it. No cast given → the `rune` cast (the main screen). Only spells given (`php cast --resonance`) → `rune` with those spells. |
| `Keeper::end()` | Turns the arcane collected in memory into `arcane.txt` and a dated copy in `arcanes/`. |
| `Aether::end()` | Adds up every Phantasm version for the footer, prints it, and **exits**. |

## Why the order matters

Begin and end are a pair: what opens first closes last. Break the order and the flow breaks with it.

- **Anything after `Aether::end()` never runs.** It calls `exit`. Put `Keeper::end()` after it and no arcane is written.
- **`Chanter::end()` must come after your casts.** It runs the cast at that moment — a cast registered later does not exist yet.
- **A rune needs the runes it leans on.** `Keeper::begin()` writes its folders with Forger. Awaken Keeper without Forger and the flow dies before it starts:

```
PHP Fatal error:  Uncaught Error: Call to undefined function Rune\Keeper\forger_fix()
```

See [Runes Lean on Runes](runes-lean-on-runes.md) for who needs whom.

## What you keep from this page

- Awaken loads. Begin opens. Cast registers. End runs.
- `Chanter::end()` → `Keeper::end()` → `Aether::end()`, always in that order.
- Next: [Runes Lean on Runes](runes-lean-on-runes.md)
