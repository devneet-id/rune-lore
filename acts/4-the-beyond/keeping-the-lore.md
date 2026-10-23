# Keeping the Lore

> When the code changes, the lore changes with it.

<!-- status: draft · sources: rune-dev/tools/lore-runes (README, gen.php, curated.json, ex/), rune-dev/notes/rune-lore-plan.md -->

`rune-lore` is how the next person learns Rune without asking. A lore that lies is worse than no lore. Keep it in step with the code.

## What is generated, what is written
| Part | How it is made |
|---|---|
| `runes/*.md` | **generated** from each rune's Phantasm + `curated.json` + `ex/<rune>.php` |
| `runites/`, `engravings/` | written by hand, from the built-in runites and `rune-dev/scenario` |
| `acts/` | written by hand, one step of the user per Act |
| `glossary.md` | written by hand — every lore word |

## Regenerate `runes/`
After any Phantasm change:
```bash
cd rune-dev/tools/lore-runes
php gen.php ../../../rune ../../../rune-lore/runes
```
`gen.php` reads every origin rune's Phantasm (version, mark, user, note, link, node) and writes one page per rune plus `runes/README.md`.

The hand-made parts come from:
- `curated.json` — per rune: `act` (where it is introduced), `lore` intro, `use` ("When to use"), `notes`.
- `ex/<rune>.php` — the "In code" example. Test it in `rune-dev/examples/lorex` before you change it.

Never edit `runes/*.md` directly — the next run overwrites it. Fix the Phantasm, `curated.json` or the example.

## Rules for writing
- English, short sentences. Lore first (1–3 sentences), then *In code*.
- Every example runs. Take it from `scenario/` or test it there.
- Every runite example starts with `#!/usr/bin/env php`.
- An Act only uses runes met so far: Act 0 — Aether, Whisper, Weaver, Chanter; Act 1 — + Forger, Cipher, Keeper; Act 2 — + Crafter; Act 3 — + Specter, Minister and your own runes.
- One page, one topic. Link, do not repeat.
- A new word goes into the [Glossary](../../glossary.md) first, with the same name as in code.
- Each page has a status line: `<!-- status: outline | draft | done · sources: ... -->`.

## When something changes
| Change in `rune` | Update in `rune-lore` |
|---|---|
| a node added/removed | regenerate `runes/`; check Acts that use it |
| a built-in runite spell | `runites/<name>.md` |
| a rename | Glossary (old → new), [Decisions](decisions.md), every page that used the old name |
| a bug fixed | remove it from [Known Issues](known-issues.md) and from "Known issue" notes in `curated.json` |
| a release | rune versions in [Versioning](versioning.md) |
