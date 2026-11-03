# Share a Project as a Relic

> Seal a runite and its files into one `.rune`, and bring it back elsewhere.

**Runes:** Keeper (+ Reliquary runite) · **From:** Act 1

```php
// carry files with the runite, then seal it
Chanter::cast('seal', function() {
  Keeper::shard(['data', 'README.md']);           // folders and files to carry
  Chanter::cast('reliquary --runite-relic')();    // → cast.rune
}, 'Seal this runite and its files into cast.rune.');
```

## How it works
- `Keeper::shard([...])` lists the files and folders that travel with the relic (`.echoes/<runite>/shard.json`) — files without extension too.
- `php cast reliquary --runite-inspect=cast.rune` shows what is inside before you trust it.
- In another folder, a fresh runite brings it back: `php cast reliquary --relic-runite=cast.rune --yes`.
- Without Keeper, the relic carries the runite only.
- To share it with everyone, list it in a reliquary ([Share It](../acts/3-liberation-of-forte/share-it.md#4--into-a-reliquary)).
