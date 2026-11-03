# Grimoire

> A book that feels alive.

Grimoire reads the **Phantasm** of every rune — so the documentation is always the code — and reveals the **arcane**, the record of what your runite did.

## Spells
| Group | Spell | Does |
|---|---|---|
| RUNIC | `grimoire --runic=Keeper` | one rune: version, note, links, every node with its note |
| RUNIC | `grimoire --runic-list` | every rune (origin runes, plus `@liberation/` runes in liberation mode); saved to `.echoes/<runite>/grimoire.json` when Keeper is engraved |
| ARCANE | `grimoire --arcane` | the arcane of the last run, step by step, with time and state |
| ARCANE | `grimoire --arcane-clean` | clears the arcane |
| | `grimoire --ai-adaptation` | a prompt that teaches an AI how Rune works (`=full` adds the source of every rune) |

Old spells answer with the new one: `--rune` → `--runic`, `--rune-all` → `--runic-list`.

## The arcane
Every rune function records a step (`aether_arcane('Keeper.entity.keeper_item_set')`). Keeper stores them in `.echoes/<runite>/arcane.txt`, with a state per step time:

`BURST` ≥0s · `FLASH` ≥0.0001s · `FLOW` ≥0.001s · `FALL` ≥2s · `BREAK` ≥5.5s · `COLLAPSE` ≥8.5s · `OVERCLOCK` ≥10s

Symbols: `λ` time · `ϟ` stopwatch · `[ϻ]` manifest · `[ͱ]` entity.

## Notes
- Without Keeper there is no arcane: `--arcane` says *No arcane recorded yet* and asks you to engrave Keeper.
- `--runic` tells you when a rune does not exist.
- Grimoire warns about runes marked `BETA` (its header still names DEPRECATED, which is no longer a mark — see [marks](../glossary.md#marks-and-signs)).
