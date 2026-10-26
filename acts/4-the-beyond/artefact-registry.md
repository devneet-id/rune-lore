# The Artefact Registry

> Any `.rune` online can become a template.

An artefact is a runite that can travel. Today four of them ship inside Rune as the Awakening templates. The plan is to let any artefact anywhere become a starting point. **This is planned — not built yet.**

## Today
- Awakening lists the files in `@bindrune/awakening/src/*.rune`:
  - Blank Starter
  - How to Casting
  - Website with Exura(SD)
  - Website with Exura(SD) to Vercel
- The file name carries the data: `Title.Date.Author.tags.rune`, URL-encoded (`Blank+Starter.2025-10-01.Anwar+Achilles.rune`).
- On choice, the RUNITE block replaces your file, the SHARDS are written next to it. An artefact made with a newer `AETHER_VERSION` is refused.

## Planned
1. **One repo per example app.** Each template (Blank Starter, Exura site, …) becomes its own repo — a real runite with its own history — and publishes its `.rune`.
2. **`rune-artefacts`** — one repo that lists `.rune` URLs. Anyone registers an artefact by adding its link.
3. **Awakening reads the registry.** Templates are no longer limited to what is inside the `rune` package; Rune fetches the list and the chosen `.rune` online.
4. **Altar** shows the same registry in a GUI ([Altar](altar.md)).

Being online is fine: Rune itself comes from Packagist, so a user without a network cannot install it either.

## Trust
An artefact is code. Before you revoke one:
```bash
php cast artefact --inspect=<file>.rune
```
It shows the runite, casts, runes, shards and system before anything is written. Revoke only what you trust. A registry adds reach, not trust.

## Make yours ready
- Keep the shebang and the sentinel markers in the runite.
- List the files it needs as shards (`Keeper::shard([...])`).
- `php cast --resonance`, then `php cast artefact --invoke`.
- See [Share It](../3-liberation-of-forte/share-it.md).
