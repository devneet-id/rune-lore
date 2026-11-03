# Install

> Composer brings the runes. Awakening writes your first runite.

Awakening is the first step out of the void. You start with an empty file and one call; Awakening fills the file with a runite.

## 1 · Requirements
- PHP (Awakening checks the minimum version and stops if yours is older)
- Composer

## 2 · Bring the runes
In a new, empty folder:
```bash
composer require devneet/rune
```
This creates `vendor/` with the ten origin runes and the built-in runites.

## 3 · The awakening file
Create a file named `cast`:
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::awakening();
```
`Rune\Ethereal::awakening()` loads the built-in runite **Awakening** from the package (`@runite/awakening/`). That is all it does — the rest happens when you run it.

## 4 · Awaken
```bash
php cast
```
```
/////////////////////////////
 A W A K E N I N G
 The Awakening of Void

Will you begin from the void,
or from a relic of the reliquary?

>>> Use a relic from devneet-id/reliquary [y/n]: n
Awakening successfully.
```
Answer **`n`**. Awakening writes the **blank** runite **over your `cast` file** (*Act. 0 - The Awakening of Void*). The awakening lines are gone; in their place is a runite with the four runes of this Act.

Answer `y` and you get the relics of [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary) to choose from by ID — How to Casting, and the Exura website relics that belong to Act 2. It needs the internet; without it, Awakening offers the blank runite. For this Act, answer `n`.

> To awaken again, put the three lines of step 3 back into `cast`.

## 5 · What you got
Open `cast`. You will recognise every part from the prologue:

| In the file | Page |
|---|---|
| `use Rune\…\Manifest as …` + `#sentinel-manifest` | [Manifest](manifest.md) |
| `X::ether()::essence()::entity();` + `#sentinel-awaken` | [Awaken](awaken.md) |
| `Aether::begin(); Chanter::begin();` … `Chanter::end(); Aether::end();` | [Begin and End](begin-and-end.md) |
| `// ✦ Main logic lives here` | where your casts go |

The first line is the shebang `#!/usr/bin/env php`, so your editor reads `cast` as PHP ([The Cast File](the-cast-file.md)). Awakening adds it whenever your file has no `.php` extension.

Its comment header says *"Act. 1 - Understanding Its Flow"*. That label is older than this lore; here, it is your Act 0.

## Nothing is remembered yet
After Awakening your folder holds `cast`, `vendor/` and the Composer files — nothing else. The four runes of this Act keep nothing between runs. Memory arrives in [Act 1 · First Resonance](../1-first-resonance/README.md).

Reference: [Awakening](../../runites/awakening.md)

Next: [Your First Runite](first-runite.md)
