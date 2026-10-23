# Decisions

> Why things are the way they are.

<!-- status: draft · sources: rune-dev/notes/rune-tasks.md (decisions, T21–T47), rune-lore.md (old names), rune-paradigm.md -->

Old names still hide in comments, Altar and old artefacts. When you meet one, this page tells you what it became and why.

## Old names → now
| Before | Now | Why |
|---|---|---|
| main file `rune.php` | `cast` | A runite is a CLI app; `php cast greet` reads like speech. Leftovers: Altar (`.echoes/rune.php/`), `ai.txt`. |
| `arise()` / `_arise()` / `_aether_end()` | `begin()` / `end()` | A pair that opens and closes the flow. `_arise` hooks still sit in some Manifests, never called (Phantasm marks them legacy). |
| `@ethereal/`, `@liberation/`, `<repo>/@bindrune/` | `@liberations/` | Three names meant liberation runes were missing from Grimoire and the footer (T22). One name now. |
| Nirvana (CSS/JS/PHP) | Exura | Rename of the web toolkit. Altar still uses Nirvana (T25). |
| `shards/` folder | `shard.json` + artefact | Shards travel inside the `.rune`; the map lives in `shard.json` (T34). |
| `chipher()` | `cipher()` | A typo fixed (T24). |
| `<runite>.json` echoes | `rune.json` | `cast.json` belonged to Specter; one fixed name avoids clashes (T21). |

## Why not React or Tailwind → Exura
Integrating React and Tailwind was tried. Both are ecosystems of their own, and Rune stopped being simple. Exura was born instead: a small toolkit that fits after [Crafter](../2-understanding-its-flow/exura.md).

## Why VOID, BETA, EXIST
VOID already covers both roles: a function held back because it is dangerous, and a function voided until it is finished. DEVELOPMENT was a search for VOID's opposite — that opposite is **EXIST**: whole and stable. BETA sits between. "Development" means developing a rune, not a mark, so DEVELOPMENT is dropped; DEPRECATED is not a mark either.

## Why liberation never replaces an origin rune
Before T42 the liberation loader was prepended: a full copy in `@liberations/Whisper/` silently replaced the real Whisper. Now the loader is appended, origin names are refused, and the rule is: need another version → a new name.

## Why one package, not many
Runes are not split into many Composer packages. The origin runes stay together; growth happens through Liberation, not through an ecosystem of packages.

## Smaller decisions you will trip on
- `Chanter::spell('x', 'v')` is read on the **next** cast — the *respell* pattern, by design (T37).
- `rune.json` stores only the repo folder name, never an absolute path (T33).
- Artefacts store OS, release, version and architecture — never the computer name (T19).
- `+` in spell values is kept (`--q=a+b` → `a+b`) (T28); `0` is a value, not "missing" (T13).
- `--phantasm-*` spells run only in liberation mode (T45).

## Still waiting for a decision
- **Float versions** — `1.10` counts as `1.1`. See [Versioning](versioning.md).
- **Where `.echoes` lives** when a runite runs from another folder (T48) — two options, see [Known Issues](known-issues.md).
