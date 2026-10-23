# Artefact

> A thing we can see.

An artefact (`.rune`) is a runite sealed into one file — its code, its echoes and its shards — so it can be shared and brought back to life anywhere.

## Spells
| Spell | Does |
|---|---|
| `artefact --invoke` | seals this runite into `<runite>.rune` |
| `artefact --inspect=<file>.rune` | shows what is inside before you use it: runite, casts, runes, shards, system |
| `artefact --revoke=<file>.rune` | brings it back: the runite replaces this file, shards are written next to it |
| `artefact --shard-list` | the shards that will travel with the artefact |
| `artefact --shard-remove=<id>` | removes one shard |
| `artefact --shard-clean` | removes every shard |

## Inside a `.rune`
```
[ᚱᚾ] ARTEFACT   who made it, when, PHP, system, Rune version
[ᚱᚾ] RUNITE     the runite
[ᚱᚾ] ECHOES     rune.json — casts, runes, size
[ᚱᚾ] SHARDS     the files listed in shard.json
```
Every block is base64, then sealed with a random runic variant (Cipher).

## Notes
- Without Keeper an artefact carries the runite only. Engrave Keeper and add shards with `Keeper::shard([...])` to carry files.
- Echoes come from `.echoes/<runite>/rune.json` (`php cast --resonance`); without it the artefact builds them itself.
- The system line keeps OS, release, version and architecture — never the computer's name.
- An artefact is a runite: revoke only what you trust.
