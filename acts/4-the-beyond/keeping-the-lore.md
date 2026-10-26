# Keeping the Lore

> When the code changes, the lore changes with it.

<!-- status: draft -->

`rune-lore` is how the next person learns Rune without asking. A lore that lies is worse than no lore. Keep it in step with the code.

## What is generated, what is written
| Part | How it is made |
|---|---|
| `runes/*.md` | **generated** from each rune's Phantasm (version, mark, user, note, link, node), plus a short lore intro, "When to use", an example and notes |
| `runites/`, `engravings/` | written by hand, from the built-in runites and runites that were run |
| `acts/` | written by hand, one step of the user per Act |
| `glossary.md` | written by hand — every lore word |

## `runes/` follows the Phantasm
The tables in `runes/*.md` are generated from each rune's Phantasm — the Phantasm is the source of truth. Change the Phantasm (and its `#NOTE`s) in `rune` first; the page follows on the next lore update. A pull request that only edits a table in `runes/` will be overwritten.

The lore intro, "When to use", the example and the notes are written by hand. Every example must run.

## Rules for writing
- English, short sentences. Lore first (1–3 sentences), then *In code*.
- Every example runs. Run it before you write it down.
- Every runite example starts with `#!/usr/bin/env php`.
- An Act only uses runes met so far: Act 0 — Aether, Whisper, Weaver, Chanter; Act 1 — + Forger, Cipher, Keeper; Act 2 — + Crafter; Act 3 — + Specter, Minister and your own runes.
- One page, one topic. Link, do not repeat.
- A new word goes into the [Glossary](../../glossary.md) first, with the same name as in code.
- Each page has a status line: `<!-- status: outline | draft | done -->`.

## When something changes
| Change in `rune` | Update in `rune-lore` |
|---|---|
| a node added/removed | its `runes/` page; check Acts that use it |
| a built-in runite spell | `runites/<name>.md` |
| a rename | Glossary (old → new), [Decisions](decisions.md), every page that used the old name |
| a bug fixed | remove it from [Known Issues](known-issues.md) and from "Known issue" notes in `runes/` |
| a release | rune versions in [Versioning](versioning.md) |
