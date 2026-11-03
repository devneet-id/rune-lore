# Rune — the main hall

> Cast nothing, and the runite shows itself.

`php cast` with no cast runs the built-in cast `rune`. It is hidden from the list — it *is* the list.

## What it shows
- **Stats** — *Main* (runite and size), *Repo* (working folder), *Rune* (how many manifests, ethers, essences and entities are awake), *Echoes* (what is kept in `.echoes/<runite>/`: Rune, Arcane, Glitch, Shards, Grimoire, Cast, Soul).
- **DEFAULT** — the built-in runites: `grimoire`, `reliquary`, `sentinel`.
- **REGISTERED** — your casts, each with its note (`≈`).
- The caption, by mode: *The Awakening of Void* · *The Liberation of Forte* · *The Federation of Fides* (the higher Act wins).

## Spells
| Spell | Does |
|---|---|
| `php cast --resonance` | also writes `.echoes/<runite>/rune.json` (casts, runes, size, memory) — read by the Reliquary |
| `php cast --zero-trust` | any cast with the arcane off and the output drained |

## The footer
```
◇Version=1.20.114: ϟExecute=0.0042s, ΞMemory=960.41KB - ^1.13MB
```
`Version=` is the version of Rune, counted from every rune's Phantasm version ([Versioning](../acts/4-the-beyond/versioning.md)) · `Execute` the time · `Memory` usage and peak.
