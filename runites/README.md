# Runites

> A **runite** is a file you engrave with runes — by default named `cast`. Rune ships with a few runites of its own, kept in `@bindrune/`. They are the tools every runite can call.

**Engraving** is the act of writing a runite: you `use` runes, awaken them, and register **casts** with Chanter.

| Built-in runite | Called with | What it does | Needs |
|---|---|---|---|
| [Awakening](awakening.md) | `Rune\Ethereal::awakening()` | turns an empty `cast` into a runite from a template (`.rune`) | — |
| [Rune](rune.md) | `php cast` | the main screen: stats, echoes, every cast with its note | Act 0 runes |
| [Grimoire](grimoire.md) | `php cast grimoire` | reads the runes (Phantasm) and the arcane | Act 0 runes (arcane: Keeper) |
| [Artefact](artefact.md) | `php cast artefact` | seals a runite into a `.rune`, inspects it, brings it back | Act 0 runes (echoes & shards: Keeper) |
| [Sentinel](sentinel.md) | `php cast sentinel` | invokes / revokes runes in your runite; liberation tools | Act 0 runes |

`Chanter::begin()` loads the casts `rune`, `grimoire`, `artefact` and `sentinel` from `@bindrune/chanter/`, so they appear under **DEFAULT** on the main screen. Your own casts appear under **REGISTERED**.

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
- Every runite keeps its memory in `.echoes/<runite>/` (when Keeper is engraved). Run a runite from its own folder.
