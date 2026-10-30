# Anatomy

> The package from the inside.

Rune looks like magic from a runite. Inside it is plain PHP: a few folders, three small core classes, and a list of files loaded in a fixed order. Know this map and nothing in Rune is hidden from you.

## The package `devneet/rune`
```
rune/
├── Ethereal.php        Rune\Ethereal — awakening(), liberation(), energy()
├── Manifest.php        Rune\Manifest — base of every Manifest: ether(), essence(), entity()
├── Phantasm.php        Rune\Phantasm — base of every Phantasm (version 0.1, mark VOID)
├── LIBERATION.md       copied to @liberations/README.md on the first liberation
├── CONTRIBUTING.md
├── composer.json       PSR-4  "Rune\\": "./"   · php >=8.1
├── Aether/ … Whisper/  the ten origin runes: Ether.php Essence.php Entity.php Manifest.php Phantasm.php
├── Crafter/weaver/     Crafter's bundle templates
└── @bindrune/
    ├── awakening/      cast.php + src/*.rune (the starter artefacts)
    └── chanter/        the built-in runites, loaded by Chanter::begin()
        ├── rune/       the main screen (cast "rune")
        ├── grimoire/   cast "grimoire" + ai.txt
        ├── sentinel/   cast "sentinel" + altar.txt + rune--*.txt templates
        └── artefact/   cast "artefact" + format*.txt
```

## The three core classes
| Class | What it does |
|---|---|
| `Rune\Manifest` | `ether()`, `essence()`, `entity()` each `require_once static::$origin . '/<Subject>.php'`, record the class in `$AETHER_RUNE_ETHER/ESSENCE/ENTITY`, and return `static::class` — that is why `X::ether()::essence()::entity()` chains. |
| `Rune\Phantasm` | Defaults for every contract: `origin`, `version = 0.1`, `main`, `user`, `note`, `mark = 'VOID'`, `link = []`, `node = []`. |
| `Rune\Ethereal` | `awakening()` requires `@bindrune/awakening/cast.php`. `liberation()` opens `@liberations/`. `energy()` hands out bit values (1, 2, 4, …). |

## Autoload — origin first
- Composer maps `Rune\` to the package folder.
- `Ethereal::liberation()` creates `@liberations/` next to the runite (the folder of `SCRIPT_FILENAME`, else `getcwd()`) (with `README.md` from `LIBERATION.md`), adds a **second** loader for `Rune\` → `@liberations/`, and registers it with `register(false)` — **appended**. Composer asks the origin loader first, so an origin rune always wins.
- It then defines `LIBERATION` (the folder path). Sentinel, Grimoire and the footer check this constant.

## How a cast travels
`php cast greet --name=Anwar`
```
require vendor/autoload.php
[Rune\Ethereal::liberation()]           optional
use Rune\X\Manifest as X;               #sentinel-manifest
X::ether()::essence()::entity();        #sentinel-awaken
Aether::begin()     gc, arcane reset, arcane "Aether.manifest.begin"
Chanter::begin()    require every @bindrune/chanter/*/cast.php → DEFAULT casts
[Keeper::begin()]   .echoes/<runite>/ + glitch handler
Chanter::cast(...)  your casts are registered, not run → REGISTERED
#sentinel-codex
Chanter::end()      read argv → pick the cast → run it
[Keeper::end()]     arcane → arcane.txt + arcanes/<date>.txt
Aether::end()       aether_exit(true): footer, then exit
```
- No arguments (`php cast`) → the cast `rune` (main screen).
- Only spells (`php cast --resonance`) → the cast `rune` with those spells.
- `--zero-trust` → arcane off, the cast runs inside a drain.
- Unknown cast → a warning and a close name (similarity ≥ 70%).

## Who knows what is awake
A rune is awake when its **main** exists: `aether_has_entity('keeper')` (function `keeper()`), `defined('KEEPER')`, `$GLOBALS['KEEPER']`. `aether_arised()` lists the awakened Manifests.

## Important constants
| Constant | Value |
|---|---|
| `AETHER_FILE` | the runite as typed (`$_SERVER['PHP_SELF']`) |
| `AETHER_REPO` | the runite's own folder (`dirname(realpath(SCRIPT_FILENAME))`, else `getcwd()`) |
| `AETHER_VERSION` | `'1.11'` — major and minor of the Rune core; `aether_version()` adds the rune versions ([Versioning](versioning.md)) |
| `AETHER_RUNE_LOCATION` | the package folder |
| `AETHER_PHP_VERSION` | `8.1.10` (minimum) |
| `KEEPER_ECHOES` | `AETHER_REPO . '/.echoes/' . basename(AETHER_FILE) . '/'` — always next to the runite |
| `LIBERATION` | the `@liberations/` path, only in liberation mode |

See also: [The Shape of a Rune](../0-the-void/shape-of-a-rune.md) · [The Flow](../2-understanding-its-flow/the-flow.md) · [Runites](../../runites/README.md)
