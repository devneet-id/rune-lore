# Rune — the main screen

> Cast nothing, and the runite shows itself.

`php cast` with no cast runs the built-in cast `rune`.

## What it shows
- **Stats** — *Main* (runite and size), *Repo* (working folder), *Rune* (how many manifests, ethers, essences and entities are awake), *Echoes* (what is kept in `.echoes/<runite>/`: Rune, Arcane, Glitch, Shards, Grimoire, Cast, Soul).
- **DEFAULT** — the built-in casts: `artefact`, `grimoire`, `rune`, `sentinel`.
- **REGISTERED** — your casts, each with its note (`≈`).
- The caption: *The Awaken from Void*, or *The Liberation of Forte* in liberation mode.

## Spells
| Spell | Does |
|---|---|
| `php cast --resonance` | also writes `.echoes/<runite>/rune.json` (casts, runes, size, memory) — read by Artefact |
| `php cast --zero-trust` | any cast with the arcane off and the output drained |

## The footer
```
◇Version=1.12.31: ϟExecute=0.0042s, ΞMemory=960.41KB - ^1.13MB
```
`Version=` is `1.` + the sum of every rune's Phantasm version · `Execute` the time · `Memory` usage and peak.
