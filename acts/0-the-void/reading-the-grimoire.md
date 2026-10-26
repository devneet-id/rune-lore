# Reading the Grimoire

> Look inside a rune you know.

<!-- status: draft -->

The Grimoire is a book that feels alive. It does not open a rune's code — it reads the rune's **Phantasm**, the picture the rune keeps of itself.

## Open it
```bash
php cast grimoire
```
It lists what it can read: `--rune`, `--rune-all`, `--arcane`, `--arcane-clean`.

## Read one rune
```bash
php cast grimoire --rune=Weaver
```
```
 #  W E A V E R —— 1.7
Built for advanced string manipulation, data binding, and template weaving—transforming raw data into structured text with flexible, context-aware logic.

  [M] Rune\Weaver\Manifest
  [O] /…/vendor/devneet/rune/Weaver
  [U] Anwar Achilles

  ::L I N K
    Aether entity 1.17

  ::N O D E
    ether
    WEAVER
      main ether
    essence
    WEAVER_BOND
      Global storage for bound template variables
      (key-value pairs)
    entity
    weaver_bind( $template, $search, String $data = "", Bool $bond = true )
      Replace a variable placeholder in a template with
      given data
    …
```

## Find the five subjects
Everything from [The Shape of a Rune](shape-of-a-rune.md) is here:

| On screen | Phantasm | Subject |
|---|---|---|
| `W E A V E R —— 1.7` | `main`, `version` | — |
| the line under it | `note` | — |
| `[M]` | the Manifest class | **Manifest** |
| `[O]` | `origin` — the rune's folder | — |
| `[U]` | `user` — who keeps the rune | — |
| `::L I N K` | `link` — the runes it leans on | — |
| `::N O D E` → `ether` | constants | **Ether** |
| `::N O D E` → `essence` | globals | **Essence** |
| `::N O D E` → `entity` | functions | **Entity** |
| `::N O D E` → `manifest` | the methods you call | **Manifest** |

The **Phantasm** is the whole page.

## Read further
```bash
php cast grimoire --rune=Whisper     # the voice: see its link to Weaver
php cast grimoire --rune-all         # all ten origin runes, one after another
```
The Grimoire reads any origin rune, even one your runite has not awakened. Look ahead at the runes of later Acts if you like — reading is free.

Write the name exactly as the rune is named (`Weaver`, not `weavers`). An unknown name stops with a PHP error today.

## Not yet: the arcane
```bash
php cast grimoire --arcane
```
```
[!] No arcane recorded yet.
 Engrave Keeper in your runite (Keeper::begin() ... Keeper::end()) to record the arcane.
```
The arcane is the trace of every step of a run. Keeping it needs memory, and memory is Keeper — the first door of the next Act.

## The prologue is done
You know what a rune is, how a runite is shaped, and how to read one. You have run very little — on purpose.

Reference: [Grimoire](../../runites/grimoire.md) · [Runes](../../runes/README.md)

Next: [Act 1 · First Resonance](../1-first-resonance/README.md)
