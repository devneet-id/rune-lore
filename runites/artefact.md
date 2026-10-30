# Artefact

> A thing we can see.

An artefact (`.rune`) is a runite sealed into one file — its code, its echoes and its shards — so it can be shared and brought back to life anywhere.

## Spells
| Spell | Does |
|---|---|
| `artefact --invoke` | seals this runite into `<runite>.rune` |
| `artefact --inspect=<file>.rune` | shows what is inside before you use it: runite, casts, runes, shards, system |
| `artefact --revoke=<file>.rune` | brings it back: the runite replaces this file, shards are written next to it |
| `artefact --inspect=<name or link> --online` | inspects an artefact from the internet |
| `artefact --revoke=<name or link> --online` | revokes an artefact from the internet |
| `--vault=<index.json url>` | with `--online`: look names up in another vault |
| `artefact --shard-list` | the shards that will travel with the artefact |
| `artefact --shard-remove=<id>` | removes one shard |
| `artefact --shard-clean` | removes every shard |

## Online: links and the vault
With `--online` the artefact comes from the internet, like a package from Composer or npm:

```bash
php cast artefact --inspect=how-to-casting --online                     # a name in the vault
php cast artefact --revoke=https://example.com/app/cast.rune --online   # a direct link
```

- **A name** is looked up in the vault: `https://raw.githubusercontent.com/devneet-id/vault/main/index.json` by default, or the index given with `--vault=`.
- **A link** is fetched as it is.
- The `.rune` is read in memory and opened at once — nothing is downloaded into your folder.

A vault index lists each artefact by name:
```json
{
  "how-to-casting": {
    "url": "https://raw.githubusercontent.com/devneet-id/how-to-casting/v1.0/cast.rune",
    "sha256": "…"
  }
}
```
When `sha256` is given, the fetched artefact must match it, or it is refused (*the seal is broken*). Anything without `[ᚱᚾ]` blocks is refused too.

PHP needs `allow_url_fopen` (or curl), and openssl for `https`.

## Inside a `.rune`
```
[ᚱᚾ] ARTEFACT   who made it, when, PHP, system, Rune version
[ᚱᚾ] RUNITE     the runite
[ᚱᚾ] ECHOES     rune.json — casts, runes, size
[ᚱᚾ] SHARDS     the files listed in shard.json
```
Every block is base64, then sealed with a random runic variant (Cipher).

## Notes
- Without Keeper an artefact carries the runite only. Engrave Keeper and add shards with `Keeper::shard([...])` to carry files. Shard paths are relative to the runite's folder, and revoke writes them next to the runite.
- The header `version=` is the version of Rune from the origin runes (`1.20.110`). An artefact made with a newer Rune is refused: *This artefact needs Rune X, you have Y.*
- Echoes come from `.echoes/<runite>/rune.json` (`php cast --resonance`); without it the artefact builds them itself.
- The system line keeps OS, release, version and architecture — never the computer's name.
- An artefact is a runite: revoke only what you trust — online artefacts most of all. Inspect first.
