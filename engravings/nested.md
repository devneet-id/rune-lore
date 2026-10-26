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
- `.echoes` is created in the folder **the command runs from**. Run each runite from its own folder:
  ```bash
  cd realm && php spire
  ```
- Running `php realm/spire` from the parent folder writes `.echoes/realm/spire/` in the parent instead — a second memory for the same runite. (Planned: `.echoes` always next to the runite, wherever it runs from.)
- The autoload path grows with the depth: `require_once __DIR__ . '/../vendor/autoload.php';`
