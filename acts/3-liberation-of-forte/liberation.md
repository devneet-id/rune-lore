# Liberation

> The Liberation of Forte — freedom in ability.

Liberation is the release of Rune from its **Origin** to its **contributors**. Full freedom is given; only the **paradigm** stays — Ether, Essence, Entity, Manifest, Phantasm. With it you can build a new working environment, a different workflow, and runes of your own: public (to contribute) or private (local).

*Forte* means freedom in ability. It is only a caption — the words you see at the entrance.

## Unlock liberation mode
Ask the Sentinel:
```bash
php cast sentinel --liberation
```
```
::S E N T I N E L
[√] The Liberation of Forte is unlocked: Rune\Ethereal::liberation();
[i] Read @liberation/README.md
```
It writes one line under the `require` line of your runite:
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::liberation();
```
Run the runite. The entrance changes from *The Awakening of Void* to:
```
 D E V N E E T  The Liberation of Forte
```
Ask again and Sentinel only tells you it is already unlocked. To close the mode, delete the line by hand.

## What it does
`Rune\Ethereal::liberation()`:
1. makes `@liberation/` **next to the runite** (wherever you cast it from), with a `README.md` greeting;
2. adds a second autoloader: `Rune\X\…` → `@liberation/X/…`;
3. defines `LIBERATION` — the path of `@liberation/`.

From then on:
- `aether_list_runes()` lists your runes (every PascalCase folder of `@liberation/`) after the ten origin runes, and their Phantasm versions join the footer `Version=`.
- Sentinel opens its **L I B E R A T I O N** spells: `--runic-create`, `--runic-delete`, `--phantasm-upgrade`, `--phantasm-repair` ([runites/sentinel.md](../../runites/sentinel.md)).

## The one law
**A liberation rune never replaces an origin rune.**
- The `@liberation/` loader is registered **after** Composer's, so `Rune\Whisper\…` always comes from the origin.
- Sentinel refuses an origin name, and a folder in `@liberation/` with one is never listed.
- Need another Whisper? Make a new rune with its own name — and only liberation runes are yours to change.

## Remember
- `@liberation/` lives next to the runite: `php lib/cast` from a parent folder finds the same runes as `php cast` inside `lib/`.
- `@liberation/` belongs to your project — it goes into git.
- Without liberation mode your runes do not exist, and the liberation spells answer *needs The Liberation of Forte*.
- Old names you may still meet: `@ethereal/`, `@liberations/` — both are now `@liberation/` (rename the folder).
- Liberation and [Federation](../4-the-beyond/reliquary.md) can be open together.
