# Runites in Sub Folders

> Group runites in folders; each keeps its memory next to itself.

**Runes:** Keeper · **From:** Act 3

```
07-nested/
├── cast              → .echoes/cast/
└── realm/
    ├── cast          → realm/.echoes/cast/
    └── spire         → realm/.echoes/spire/
```

## How it works
- `.echoes` is always created next to the runite. `cd realm && php spire` and `php realm/spire` from the parent use the same `realm/.echoes/spire/`.
- The autoload path grows with the depth: `require_once __DIR__ . '/../vendor/autoload.php';`
