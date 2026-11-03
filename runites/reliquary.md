# Reliquary

> A place where relics are kept.

A **relic** (`.rune`, once called *artefact*) is a runite preserved to travel — its code, its echoes and its shards in one file — so it can be shared and brought back to life anywhere. The **Reliquary** runite makes relics, opens them, and reads the reliquaries of Rune online.

## Spells
| Group | Spell | Does |
|---|---|---|
| RUNITE | `reliquary --runite-inspect[=<file>.rune]` | shows what is inside a relic before you open it: runite, casts, runes, shards, system (default: `<runite>.rune`) |
| RUNITE | `reliquary --runite-relic` | seals this runite into `<runite>.rune`, next to it |
| SHARD | `reliquary --shard=<id>` | inspects one shard |
| SHARD | `reliquary --shards` | the shards that will travel with the relic |
| SHARD | `reliquary --shard-remove=<id>` | removes one shard |
| SHARD | `reliquary --shard-clean` | removes every shard |
| RELIC | `reliquary --relic-runite[=<vendor>/<repo>]` | opens a relic into this runite: the runite is replaced, shards are written next to it. Empty = `<runite>.rune`. Asks `[y/n]` first; `--yes` skips it, `--tag=<version>` picks a version (default: the newest) |
| RELIC | `reliquary --relic=<vendor>/<repo>` | one relic of the reliquary: repo, runite, note, every version |
| RELIC | `reliquary --relics` | every relic of the reliquary |
| FEDERATION | `reliquary --initiate --repo=<you>/reliquary` | uses your own reliquary |
| FEDERATION | `reliquary --discover` | follows the chain of reliquaries and records every relic |
| FEDERATION | `reliquary --retrieve=<vendor>/<repo>` | keeps a relic in `@federation/<vendor>/<repo>@<tag>.rune` (`--tag=`) |

The FEDERATION group shows only in federation mode ([below](#federation)).

## Online: the reliquary
Without federation, every relic comes from [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary):

```bash
php cast reliquary --relics
php cast reliquary --relic=devneet-id/how-to-casting
php cast reliquary --relic-runite=devneet-id/how-to-casting
```

A reliquary is a GitHub repo with two files, read from `raw.githubusercontent.com` (no API limit):
```json
// relic.json — the relics of its owner
{ "main": "devneet-id/reliquary",
  "list": { "devneet-id/how-to-casting": {
    "repo": "https://github.com/devneet-id/how-to-casting", "runite": "cast", "note": "…",
    "tags": { "0.1.0": { "url": "…/cast.rune", "sha256": "…", "rune": "1.11", "ref": "main@eacbec9" } } } } }

// nexus.json — the forks that keep relics of their own
{ "main": "devneet-id/reliquary",
  "list": { "<owner>/reliquary": { "owner": "<owner>", "branch": "main", "relic": "relic.json", "nexus": "nexus.json" } } }
```
- A reliquary only lists the relics of its owner (`<owner>/*`).
- Every download must match its `sha256`, or it is refused (*the seal is broken*). Anything without `[ᚱᚾ]` blocks is refused too.
- PHP needs `allow_url_fopen` (or curl), and openssl for `https`.

## Federation
*The Federation of Fides*: every reliquary stands on its own, yet they are connected — forks of forks. Unlock it with `php cast sentinel --federation`.

```bash
php cast reliquary --initiate --repo=<you>/reliquary     # your reliquary becomes the main one
php cast reliquary --discover                            # follow nexus.json from yours and devneet-id/reliquary
php cast reliquary --retrieve=devneet-id/how-to-casting  # keep it in @federation/
php cast reliquary --relic-runite=devneet-id/how-to-casting
```

```
@federation/
├── devneet-id/how-to-casting@0.1.0.rune
├── federation.json
└── README.md
```
`federation.json` records your reliquary and every relic found:
```json
{ "updated": "2026-11-01T10:05:00Z",
  "reliquary": { "main": "<you>/reliquary", "list": { "devneet-id/how-to-casting": { "repo": "…", "tags": { … } } } } }
```
- `--discover` replaces the list; `--relic`, `--relics` and `--relic-runite` add to it. Nothing is recorded outside federation mode.
- `--relic-runite=<vendor>/<repo>` looks in `@federation/` first, then online.
- Without `main` (no `--initiate` yet), the reliquary is `devneet-id/reliquary`.

## Inside a `.rune`
```
The Relic of Runite
[ᚱᚾ] RELIC      who made it, when, PHP, system, Rune version
[ᚱᚾ] RUNITE     the runite
[ᚱᚾ] ECHOES     rune.json — casts, runes, size
[ᚱᚾ] SHARDS     the files listed in shard.json
```
Every block is base64, then sealed with a random runic variant (Cipher). The first line is only a title; the block names are what is read. Older relics with an `ARTEFACT` block still open.

## Notes
- Without Keeper a relic carries the runite only. Engrave Keeper and add shards with `Keeper::shard([...])` to carry files — a file without extension (like `cast`) too. Shard paths are relative to the runite's folder, and opening a relic writes them next to the runite.
- The header `version=` is the version of Rune from the origin runes (`1.20.114`). A relic made with a newer Rune is refused: *This relic needs Rune X, you have Y.* Rune 1.12.x can not open relics with a `RELIC` block.
- Echoes come from `.echoes/<runite>/rune.json` (`php cast --resonance`); without it the relic builds them itself.
- The system line keeps OS, release, version and architecture — never the computer's name.
- A relic is a runite: open only what you trust — online relics most of all. Inspect first.
- `php cast artefact …` still answers, with the new spell (*`artefact --invoke` is now `reliquary --runite-relic`*).
