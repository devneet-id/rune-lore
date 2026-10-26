# Nested Runites

> Apps inside subfolders.

<!-- status: draft -->

Runites can live in subfolders, grouped by realm. Each keeps its memory next to itself — as long as you call it from its own folder.

```
07-nested/
├── cast              → .echoes/cast/
└── realm/
    ├── cast          → realm/.echoes/cast/
    └── spire         → realm/.echoes/spire/
```

## The autoload path grows
```php
require_once __DIR__ . '/../vendor/autoload.php';   // realm/spire
```

## Run from its own folder
```bash
cd realm && php spire
```
Today `.echoes` (and `@liberations/`) follow the folder **the command runs from**, not the runite (`AETHER_REPO = getcwd()`):

| Command | Memory written to |
|---|---|
| `cd realm && php spire` | `realm/.echoes/spire/` ✓ |
| `php realm/spire` (from the parent) | `.echoes/realm/spire/` — a second memory |

A runite in liberation mode cast from another folder is worse: its runes are not found, and an empty `@liberations/` appears in that folder.

**Planned:** `.echoes` always next to its runite, wherever it is run from. Until then: one runite, one folder to run it from.

## A runite that visits another
From the parent, cast an inner runite **inside its folder**:
```php
$command = 'cd ' . escapeshellarg(__DIR__ . '/realm') . ' && ' . escapeshellarg(PHP_BINARY) . ' spire where';
```
This is what scenario 07's `visit` cast does.
