# Nested Runites

> Apps inside subfolders.

Runites can live in subfolders, grouped by realm. Each keeps its memory next to itself, wherever it is cast from.

```
app/
├── cast              → .echoes/cast/
└── realm/
    ├── cast          → realm/.echoes/cast/
    └── spire         → realm/.echoes/spire/
```

## The autoload path grows
```php
require_once __DIR__ . '/../vendor/autoload.php';   // realm/spire
```

## Cast from anywhere
`AETHER_REPO` is the runite's own folder, so both commands use the same memory:

| Command | Memory |
|---|---|
| `cd realm && php spire` | `realm/.echoes/spire/` |
| `php realm/spire` (from the parent) | `realm/.echoes/spire/` — the same one |

A runite in liberation mode finds its `@liberations/` the same way, next to itself.

## A runite that visits another
From the parent, cast an inner runite by its path:
```php
$command = escapeshellarg(PHP_BINARY) . ' ' . escapeshellarg(__DIR__ . '/realm/spire') . ' where';
```
