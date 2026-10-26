# Phantasm

> Every rune carries its contract.

<!-- status: draft -->

The Phantasm is how a rune speaks of itself without being run. The Grimoire reads it, the footer counts it, and other runes find it through it. Rune uses it instead of PHP Reflection.

## The fields
| Field | Holds | Who writes it |
|---|---|---|
| `version` | the rune's version | `--create-rune` (0.1), then `--phantasm-up` |
| `main` | the rune's name | `--create-rune` |
| `user` | who shapes it | you |
| `note` | its purpose, one sentence | you |
| `mark` | `VOID`, `BETA`, `EXIST` ([marks](../../glossary.md#marks-and-signs)) | `--create-rune` (BETA), then you |
| `link` | the runes it leans on: `[rune, parts, version]` | `--phantasm-fix-link` |
| `node` | every constant, global, function and method, with its `#NOTE` | `--phantasm-fix-node` + `--phantasm-fix-note` |
| `origin` | the rune's folder (`__DIR__`) | `--create-rune` — keep it |

`user` and `note` are not in the generated file. Add them by hand:
```php
  public $user = 'Anwar';

  public $note = 'Keeps a small ledger of income and expense in one flow.';
```

## Fix it from the code
After you [engrave](engrave-a-rune.md) the five files, let Sentinel read them:
```bash
php cast sentinel --phantasm-fix=ledger
```
```
SENTINEL :: Phantasm Fix Auto
[√] Node fixed for phantasm: Ledger
[√] Link fixed for phantasm: Ledger
[√] Note fixed for phantasm: Ledger
[√] Update phantasm: Ledger
```
`--phantasm-fix` = node + link + note + version up, in that order. Ledger's Phantasm now holds:
```php
  public $version = '0.2';

  public $link = [
    ['Weaver', 'entity', '1.7'],
    ['Aether', 'entity', '1.17'],
  ];

  public $node = [
    [
      'type' => 'ether',
      'call' => 'LEDGER_CURRENCY',
      'note' => 'The currency written before every amount.',
    ],
    // … every Ether, Essence, Entity and Manifest node
  ];
```
- **Node** reads `define(...)`, `$GLOBALS[...]`, functions that carry the rune's name, and static methods. Commented code is skipped.
- **Link** finds which runes your code calls: `weaver_bind_multiple()` → Weaver, `aether_arcane()` → Aether.
- **Note** copies the `#NOTE:` above each node. No note, empty note — write them.

One step at a time: `--phantasm-fix-node=`, `--phantasm-fix-link=`, `--phantasm-fix-note=`. `--phantasm-fix-link-all` relinks **every** rune, origin runes too — that is maintainer work ([Act 4](../4-the-beyond/README.md)).

## Raise the version
Every change raises the Phantasm of the rune that changed:
```bash
php cast sentinel --phantasm-up=ledger
```
`0.2` → `0.3`. The minor number grows by one. The footer follows, because it is `1.` + the sum of every Phantasm version:
```
◇Version=1.12.51   Ledger 0.2
◇Version=1.12.61   Ledger 0.3
```
**Known issue:** after `.9` comes `.10` (`0.9` → `0.10`), but the footer adds versions as numbers, so `0.10` counts as `0.1` and the footer drops (`1.13.21` → `1.12.41`). Until this is fixed, plan your versions around it.

## The mark
`BETA` while it settles. Change it by hand: `VOID` for a rune that is held back or returns nothing on purpose, `EXIST` when it is whole and stable — the opposite of VOID. A rune moves VOID → BETA → EXIST. The Grimoire warns about BETA.

Next: [Use Your Rune](use-your-rune.md).
