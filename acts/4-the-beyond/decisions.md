# Decisions

> Why things are the way they are.

Old names still hide in comments, Altar and old relics. When you meet one, this page tells you what it became and why.

## Old names → now
| Before | Now | Why |
|---|---|---|
| main file `rune.php` | `cast` | A runite is a CLI app; `php cast greet` reads like speech. Leftovers: Altar (`.echoes/rune.php/`), `ai.txt`. |
| `arise()` / `_arise()` / `_aether_end()` | `begin()` / `end()` | A pair that opens and closes the flow. `_arise` hooks still sit in some Manifests, never called (Phantasm marks them legacy). |
| `@ethereal/`, `@liberations/`, `<repo>/@bindrune/` | `@liberation/` | Many names meant liberation runes were missing from Grimoire and the footer. One name now, singular like every mode folder (`@federation/`). |
| `@bindrune/` (and `@bindrune/chanter/`) | `@runite/` | The built-in runites are runites; one flat folder, no special case when listing runes. |
| artefact, `artefact` cast | relic, `reliquary` cast | *Artifact* is a common word with the same idea; a *relic* is what a *reliquary* keeps. Old `.rune` files with an `ARTEFACT` block still open. |
| `--invoke`, `--create-rune`, `--phantasm-fix`, `--rune` … | `--runite-insert`, `--runic-create`, `--phantasm-repair`, `--runic` … | Spells use system words (insert, create, list, repair…); lore words stay in the names of runites and things. Old spells answer with the new name. |
| starter templates in the package | relics in `devneet-id/reliquary` | Any relic online can be a starting point; the package stays small. |
| Nirvana (CSS/JS/PHP) | Exura | Rename of the web toolkit. Altar still uses Nirvana. |
| `shards/` folder | `shard.json` + relic | Shards travel inside the `.rune`; the map lives in `shard.json`. |
| `chipher()` | `cipher()` | A typo fixed. |
| `<runite>.json` echoes | `rune.json` | `cast.json` belonged to Specter; one fixed name avoids clashes. |

## Why not React or Tailwind → Exura
Integrating React and Tailwind was tried. Both are ecosystems of their own, and Rune stopped being simple. Exura was born instead: a small toolkit that fits after [Crafter](../2-understanding-its-flow/exura.md).

## Why VOID, BETA, EXIST
VOID already covers both roles: a function held back because it is dangerous, and a function voided until it is finished. DEVELOPMENT was a search for VOID's opposite — that opposite is **EXIST**: whole and stable. BETA sits between. "Development" means developing a rune, not a mark, so DEVELOPMENT is dropped; DEPRECATED is not a mark either.

## Why liberation never replaces an origin rune
Before, the liberation loader was prepended: a full copy in `@liberation/Whisper/` silently replaced the real Whisper. Now the loader is appended, origin names are refused, and the rule is: need another version → a new name.

## Why one package, not many
Runes are not split into many Composer packages. The origin runes stay together; growth happens through Liberation, not through an ecosystem of packages.

## Smaller decisions you will trip on
- `Chanter::spell('x', 'v')` is read on the **next** cast — the *respell* pattern, by design.
- `rune.json` stores only the repo folder name, never an absolute path.
- Relics store OS, release, version and architecture — never the computer name.
- `+` in spell values is kept (`--q=a+b` → `a+b`) `0` is a value, not "missing".
- `--phantasm-*` spells run only in liberation mode.

## Decided since
- **Whole-number versions** — a version is `<major>.<minor>` read as whole numbers, so `1.10` comes after `1.9`. See [Versioning](versioning.md).
- **`.echoes` next to the runite** — `AETHER_REPO` is the runite's own folder, so `.echoes`, the mode folders and shards stay with it, wherever it is cast from.
- **Modes are unlocked by Sentinel** — `sentinel --liberation` / `--federation` write one line under `require`; there is no toggle, so closing a mode is a deliberate edit.
- **Mode folders go into git** — `@liberation/` and `@federation/` belong to the project; `sentinel --gitignore` hides only `vendor/` and every `.echoes/`.
- **Federation without an argument** — `Rune\Ethereal::federation()` only marks the mode; your reliquary lives in `@federation/federation.json` (`reliquary --initiate`), not in the runite.
- **A required spell in `arg`, an optional one in `echo`** — every built-in runite writes its casts this way.
