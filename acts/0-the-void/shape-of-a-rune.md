# The Shape of a Rune

> Every rune is one folder of five files.

<!-- status: draft · sources: rune-paradigm.md §3–4, rune README (Paradigm), Rune/Whisper/*, Rune/Manifest.php, Rune/Phantasm.php -->

A rune is like a living thing. It has truth that never changes, a state that flows, a will that acts, a face it shows, and a shadow that tells you what it is.

## The folder
```
Whisper/
├── Ether.php       truth
├── Essence.php     flow
├── Entity.php      will
├── Manifest.php    face
└── Phantasm.php    shadow
```
Every origin rune — and every rune you make later — has exactly these five files, in namespace `Rune\<Name>`.

## The five subjects
| Subject | Lore | In code | Example from Whisper |
|---|---|---|---|
| **Ether** | something that never changes but always has meaning | constants: `define(...)` | `define('WHISPER', true);` |
| **Essence** | something that can change as time goes on | globals: `$GLOBALS[...]` | `$GLOBALS['WHISPER_COLORS']` |
| **Entity** | something that makes other things change | functions: `rune_xxx()` — all the logic | `function whisper_echo(...)` |
| **Manifest** | a box that connects things so they work together | a static class `Rune\X\Manifest` | `Whisper::echo(...)` |
| **Phantasm** | a picture in the mind, to understand | a class `Rune\X\Phantasm` — the contract | version, note, link, node |

## How they lean on each other
```
            Phantasm  ── describes ──▶  everything below
               │
  your runite ─┴─▶  Manifest  ──▶  Entity  ──▶  Essence
                                     │             │
                                     └──▶  Ether ◀─┘
```
- **Your runite speaks only to the Manifest.** `Whisper::echo('hi')` is the Manifest.
- **The Manifest holds no logic.** It forwards to the Entity: `Whisper::echo()` calls `whisper_echo_set()`.
- **Entities do the work.** They read Ether and Essence, and may call the entities of other runes — this is how runes work together.
- **The Phantasm describes it all**, so tools can read a rune without opening its code.

## The Phantasm
The Phantasm is the rune's contract. It replaces PHP Reflection: instead of inspecting code at run time, Rune reads what the rune says about itself.

```php
class Phantasm extends \Rune\Phantasm {
  public $origin  = __DIR__;
  public $version = '1.13';
  public $main    = 'Whisper';
  public $user    = 'Anwar Achilles, Kuro Kid';
  public $note    = 'Handles user-facing output through styled messages, prompts, and echoes…';
  public $link    = [['Aether', 'entity', '1.17'], ['Weaver', 'entity', '1.7']];
  public $node    = [ /* every ether, essence, entity and manifest, with its note */ ];
}
```
`mark` is not written here, so Whisper keeps the default from `\Rune\Phantasm`: `VOID`. *A rune without a Phantasm is a rune nobody knows.* You will read Phantasms yourself in [Reading the Grimoire](reading-the-grimoire.md).

Full tables of every node: [Runes](../../runes/README.md).

Next: [The Cast File](the-cast-file.md)
