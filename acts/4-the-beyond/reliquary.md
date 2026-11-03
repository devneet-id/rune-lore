# The Reliquary

> Any relic, anywhere — kept by reliquaries that trust each other.

A relic is a runite that can travel. A **reliquary** is where relics are kept online: a GitHub repo that lists them. The first one is [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary); every fork can become a reliquary of its own. Together they are *The Federation of Fides*.

→ Reference: [runites/reliquary.md](../../runites/reliquary.md)

## What lives in a reliquary
```
<owner>/reliquary
├── relic.json     the relics of its owner: <owner>/<repo> → repo, runite, note, tags
├── nexus.json     the forks that keep relics of their own
└── README.md
```
```json
{ "main": "devneet-id/reliquary",
  "list": { "devneet-id/how-to-casting": {
    "repo": "https://github.com/devneet-id/how-to-casting", "runite": "cast",
    "note": "Learn how to cast: casts, spells, and cast in cast.",
    "tags": { "0.1.0": { "url": "…/cast.rune", "sha256": "…", "rune": "1.11", "ref": "main@eacbec9" } } } } }
```
- **One repo per relic.** Each app (How to Casting, an Exura site, yours) is its own repo with its own history, and publishes its `.rune` per version.
- **A reliquary lists only its owner.** `devneet-id/reliquary` lists `devneet-id/*`; your fork lists `<you>/*`. Names of others in a fork are ignored.
- **The seal.** Each version carries the `sha256` of its `.rune`; Rune refuses a download that does not match.
- Rune reads the raw files (`raw.githubusercontent.com`) — no API, no limit.

## Without federation
Every runite already reads `devneet-id/reliquary`:
```bash
php cast reliquary --relics
php cast reliquary --relic-runite=devneet-id/how-to-casting
```
[Awakening](../../runites/awakening.md) offers the same relics when a runite is born. Nothing is written to your folder but the runite and its shards.

## With federation — your own reliquary
```bash
php cast sentinel --federation                            # unlock: Rune\Ethereal::federation();
php cast reliquary --initiate --repo=<you>/reliquary      # your fork is the main reliquary
php cast reliquary --discover                             # walk the chain, record every relic
php cast reliquary --retrieve=devneet-id/how-to-casting   # keep one in @federation/
```
- `--discover` starts from your reliquary and from `devneet-id/reliquary`, follows every `nexus.json` (forks of forks, each read once), and writes every relic found into `@federation/federation.json`.
- `--retrieve` keeps a version as `@federation/<vendor>/<repo>@<tag>.rune`; `--relic-runite` uses it before going online.
- `@federation/` belongs to your project — it goes into git, so your team opens the same relics.

## Add your relic
1. Fork `devneet-id/reliquary` (or use your fork).
2. In your app's repo: `php cast reliquary --runite-relic`, commit `cast.rune`, tag a version.
3. In your reliquary's `relic.json`: add `<you>/<repo>` with the raw link to the tagged `.rune` and its `sha256`.
4. To be found by others, ask the reliquary you forked from to add yours to its `nexus.json`.

## Trust
A relic is code. Before you open one:
```bash
php cast reliquary --relic=<vendor>/<repo>
php cast reliquary --retrieve=<vendor>/<repo>
php cast reliquary --runite-inspect=@federation/<vendor>/<repo>@<tag>.rune
```
The seal proves the file is the one the reliquary listed — not that its author is kind. A reliquary adds reach, not trust.

## Make yours ready
- Keep the shebang and the sentinel markers in the runite.
- List the files it needs as shards (`Keeper::shard([...])`).
- `php cast --resonance`, then `php cast reliquary --runite-relic`.
- See [Share It](../3-liberation-of-forte/share-it.md).
