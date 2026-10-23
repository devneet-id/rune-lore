# Liberation

> The Liberation of Forte — freedom in ability.

<!-- status: draft · sources: rune/LIBERATION.md, rune/README.md (Liberation, Laws), Ethereal.php, Aether/Entity.php · tested in rune-dev/scenario (scratch) -->

Liberation is the release of Rune from its **Origin** to its **contributors**. Full freedom is given; only the **paradigm** stays — Ether, Essence, Entity, Manifest, Phantasm. With it you can build a new working environment, a different workflow, and runes of your own: public (to contribute) or private (local).

*Forte* means freedom in ability. It is only a caption — the words you see at the entrance.

## Enter liberation mode
One line, right after the autoload:
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::liberation();
```
Run the runite. The entrance changes from *The Awaken from Void* to:
```
 D E V N E E T  The Liberation of Forte
```

## What it does
`Rune\Ethereal::liberation()`:
1. makes `@liberations/` in the **current folder** (`getcwd()`), with a `README.md` copied from Rune's `LIBERATION.md`;
2. adds a second autoloader: `Rune\X\…` → `@liberations/X/…`;
3. defines `LIBERATION` — the path of `@liberations/`.

From then on:
- `aether_list_runes()` lists your runes after the ten origin runes, and their Phantasm versions join the footer `Version=`.
- Sentinel opens its **L I B E R A T I O N** spells: `--create-rune`, `--remove-rune`, `--phantasm-up`, `--phantasm-fix…` ([runites/sentinel.md](../../runites/sentinel.md)).

## The one law
**A liberation rune never replaces an origin rune.**
- The `@liberations/` loader is registered **after** Composer's, so `Rune\Whisper\…` always comes from the origin.
- Sentinel refuses an origin name, and skips a folder in `@liberations/` that has one.
- Need another Whisper? Make a new rune with its own name — and only liberation runes are yours to change.

## Remember
- `@liberations/` follows the folder you run from. Run the runite from its own folder: from anywhere else your runes are not found (`Class "Rune\Ledger\Manifest" not found`) and an empty `@liberations/` appears there.
- Without `Rune\Ethereal::liberation()` your runes do not exist, and the liberation spells answer *You are not eligible!!*
- Old names you may still meet: `@ethereal/`, `@liberation/` — both are now `@liberations/`.
