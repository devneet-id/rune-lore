# Share a Project as an Artefact

> Seal a runite and its files into one `.rune`, and bring it back elsewhere.

**Runes:** Keeper (+ Artefact runite) · **From:** Act 1

```php
// carry files with the runite, then seal it
Chanter::cast('seal', function() {
  Keeper::shard(['data', 'README.md']);       // folders and files to carry
  Chanter::cast('artefact --invoke')();       // → cast.rune
}, 'Seal this runite and its files into cast.rune.');
```

## How it works
- `Keeper::shard([...])` lists the files and folders that travel with the artefact (`.echoes/<runite>/shard.json`).
- `php cast artefact --inspect=cast.rune` shows what is inside before you trust it.
- In another folder, a fresh runite brings it back: `php cast artefact --revoke=cast.rune`.
- Without Keeper, the artefact carries the runite only.
