# Paradigm

> Runes are the core. Runites are what you build from them.

The only thing that never changes in Rune is its paradigm. Everything else is free.

## One rune, one purpose
A rune does one thing. Whisper speaks, Weaver shapes text, Chanter listens to the command line. A rune is never stretched to do another rune's work — when you need something new, it becomes a new rune.

## Runes and runites
| | **Runes** | **Runites** |
|---|---|---|
| What | the core building blocks | the apps you build from them |
| Where | the `devneet/rune` package | your project — a file named `cast` |
| You | call them | engrave them |

Writing a runite is called **engraving**. The built-in tools you will meet — Awakening, the main screen, Grimoire — are runites too, engraved by Rune's creator from the same runes you use. See [Runites](../../runites/README.md).

## The ten origin runes
| Rune | In one line | Act |
|---|---|---|
| [Aether](../../runes/aether.md) | the flow beneath everything | **0** |
| [Whisper](../../runes/whisper.md) | the voice to the user | **0** |
| [Weaver](../../runes/weaver.md) | text and templates | **0** |
| [Chanter](../../runes/chanter.md) | the command line | **0** |
| [Forger](../../runes/forger.md) | files and folders | 1 |
| [Cipher](../../runes/cipher.md) | secrets | 1 |
| [Keeper](../../runes/keeper.md) | memory | 1 |
| [Crafter](../../runes/crafter.md) | the builder | 2 |
| [Specter](../../runes/specter.md) | beyond the main process | 3 |
| [Minister](../../runes/minister.md) | speaks with a familiar | 3 |

This Act needs only the first four. With them a runite can flow, speak, shape text and answer commands. It cannot touch files or remember anything yet — that is the next Act.

## Rune is not standalone
Aether flows through every rune. Every other rune leans on it, and some lean on each other: Whisper uses Weaver to fill its `{{tokens}}`. That is by design. You will see what happens when one is missing in [Awaken](awaken.md).

## Lore name = code name
`Whisper` in the lore is `Rune\Whisper\Manifest` in code. A **cast** in the lore is `Chanter::cast()` in code. When a word is new, look it up in the [Glossary](../../glossary.md) — never guess from a generic meaning.

Next: [The Shape of a Rune](shape-of-a-rune.md)
