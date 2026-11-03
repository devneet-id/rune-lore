# Awakening

> From the silence of nothingness, echoes rise from the void.

Awakening turns an empty file into a runite. It asks one question — *begin from the void, or from a relic of the reliquary?* — then writes the chosen runite into your file.

## In code
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::awakening();
```
```bash
php cast
```

## The flow
1. **A W A K E N I N G** · *The Awakening of Void* — *Use a relic from devneet-id/reliquary [y/n]*
   - `n` → the **blank template** (`@runite/awakening/blank.txt`, *Act. 0 - The Awakening of Void*): the four runes of Act 0.
   - `y` → the relics of [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary), each with its newest version, the Rune it needs and its note:
     ```
     [1] devneet-id/how-to-casting @0.1.0 [rune 1.11]
      :: Learn how to cast: casts, spells, and cast in cast.
     ```
2. The chosen relic is downloaded, checked against its sha256 and opened: its **runite** replaces your file (starting with `#!/usr/bin/env php` when your file has no `.php`), its **shards** are written next to it.
3. *Awakening successfully. Checkout your runite with `php cast`.*

## Notes
- When the reliquary can not be reached (offline, no openssl), Awakening says so and offers the blank template.
- A relic made with a newer Rune than yours is refused.
- After awakening, the file is no longer the awakening door — it is your runite. To awaken again, put the three lines above back.
- The starter relics (How to Casting, Website with Exura…) live in `devneet-id/reliquary`, not in the package: anyone can add one there — see [The Reliquary](../acts/4-the-beyond/reliquary.md).
