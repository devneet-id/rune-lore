# Glossary

> Every lore word with its technical meaning. The lore name is always the name in code — learn it once here.

Words are grouped by where you meet them. Each one gives its **lore** meaning first, then what it is **in code**.

- [The world](#the-world) · [The five subjects](#the-five-subjects) · [Works and things](#works-and-things) · [Reading and guarding](#reading-and-guarding) · [Spell words](#spell-words) · [Marks and signs](#marks-and-signs) · [Template tokens](#template-tokens) · [Acts](#acts) · [Old names](#old-names)

---

## The world

| Word | Lore | In code |
|---|---|---|
| **Rune** | One power, one purpose. | A folder in namespace `Rune\<Name>` with five files: Ether, Essence, Entity, Manifest, Phantasm. → [Runes](runes/README.md) |
| **Origin rune** | The ten runes Rune was born with. | The runes in the `devneet/rune` package: [Aether](runes/aether.md), [Whisper](runes/whisper.md), [Weaver](runes/weaver.md), [Chanter](runes/chanter.md), [Forger](runes/forger.md), [Cipher](runes/cipher.md), [Keeper](runes/keeper.md), [Crafter](runes/crafter.md), [Specter](runes/specter.md), [Minister](runes/minister.md). |
| **Ethereal** | The place of what is not yet known. | The core class `Rune\Ethereal`: `awakening()`, `liberation()`, `federation()`, `energy()`. |
| **Aether** | The flow beneath everything. | The first rune to begin and the last to end: paths, time, memory, `dd`, arcane, the version footer. → [Aether](runes/aether.md) |
| **Runite** (built-in) | The runites Rune carries. | The `@runite/` folder in the package: `awakening/`, `rune/`, `grimoire/`, `sentinel/`, `reliquary/`. Once called *Bindrune* (`@bindrune/`). → [Runites](runites/README.md) |
| **Liberation** | Runes of your own, set free. | Unlocked by `sentinel --liberation`. The `@liberation/` folder in your project. Its runes load through `Rune\` with a loader registered after Composer's (so origin runes always win), and `LIBERATION` is defined. A liberation rune **never replaces an origin rune**. → [Act 3](acts/3-liberation-of-forte/README.md) |
| **Forte** | Freedom in ability. | Only a caption: *"The Liberation of Forte"*, shown in liberation mode. Not a feature. |
| **Federation** | Reliquaries that trust each other. | Unlocked by `sentinel --federation`: `Rune\Ethereal::federation();`, the `@federation/` folder with `federation.json` and kept relics; your own reliquary (`reliquary --initiate`) and the chain of forks (`--discover`). → [The Reliquary](acts/4-the-beyond/reliquary.md) |
| **Fides** | Trust. | Only a caption: *"The Federation of Fides"*, shown in federation mode. The trust is kept by the seal (sha256). |
| **Void** | Where everything begins. | Only a caption: *"The Awakening of Void"*, shown when no mode is open. |
| **Echoes** | Voices from the past — the memory of a runite. | The `.echoes/<runite>/` folder kept by Keeper: items, arcane, glitch, `shard.json`, `rune.json`, `soul.json`. → [Keeper](runes/keeper.md) |
| **Exura** | A simple toolkit for the web. | ExuraCSS / ExuraJS / ExuraPHP. Born because React and Tailwind are ecosystems of their own and did not stay simple inside Rune. Met after Crafter. → [Act 2](acts/2-understanding-its-flow/README.md) |
| **Altar** | The place where runites are shaped by hand. | A development GUI (`sentinel --altar`, `127.0.0.1:8100`) — **still 100% in development**. Planned: edit runites, help build websites, a readable Grimoire, make and inspect relics, browse the reliquaries. → [Altar](acts/4-the-beyond/altar.md) |

## The five subjects

Every rune is made of these five files. → [Runes](runes/README.md)

| Word | Lore | In code |
|---|---|---|
| **Ether** | Truth that never changes. | `Ether.php` — constants, e.g. `AETHER_REPO`, `KEEPER_ECHOES`. |
| **Essence** | State that changes as the flow goes on. | `Essence.php` — globals, e.g. `$CHANTER_CAST`. |
| **Entity** | The logic. | `Entity.php` — functions, e.g. `forger_fix()`. Other runes call them too. |
| **Manifest** | The face a rune shows. | `Manifest.php` — the static class your runite calls: `Forger::fix(...)`. |
| **Phantasm** | The contract of a rune. | `Phantasm.php` — `version`, `main`, `user`, `note`, `mark`, `link`, `node`, `origin`. Read it with `grimoire --runic=X`. |

## Works and things

| Word | Lore | In code |
|---|---|---|
| **Engraving** | The act of carving runes — coding. | A verb, not a folder: writing a runite with `use`, awakening runes, and `Chanter::cast(...)`. → [Engravings](engravings/README.md) (recipes) |
| **Runite** | What an engraving makes — your app. | A file engraved with runes. Any name; the default is `cast`. Without `.php` it must start with `#!/usr/bin/env php`. `AETHER_FILE` is its name. → [Runites](runites/README.md) |
| **Arise / awaken** | To wake a rune. | `X::ether()::essence()::entity();` — under the `#sentinel-awaken` marker. |
| **Cast** | A command spoken to the runite. | A CLI command: `Chanter::cast('name --spell', fn, 'echo')`. Also a common name for the runite file. |
| **Spell** | A word that shapes a cast. | A CLI option `--x` or `--x=value`, read with `Chanter::spell('x')`: `false` when missing, `'1'` when given without a value. |
| **Echo** (of a cast) | What a cast says of itself. | The third argument of `Chanter::cast()` — the `≈` line on the main hall. |
| **Relic** | A runite preserved to travel. | A `.rune` file: runite (+ echoes + shards) in base64, then sealed with the runic cipher. Blocks start with `[ᚱᚾ]`. Once called *artefact*. → [reliquary](runites/reliquary.md) |
| **Reliquary** | A place where relics are kept. | The built-in runite `reliquary`, and a GitHub repo listing relics (`relic.json`, `nexus.json`) — first of all `devneet-id/reliquary`. → [The Reliquary](acts/4-the-beyond/reliquary.md) |
| **Nexus** | The links between reliquaries. | `nexus.json` in a reliquary: the forks that keep relics of their own. `reliquary --discover` follows it. |
| **Shard** | A piece carried with the runite. | A file that travels inside the relic, listed in `.echoes/<runite>/shard.json` by `Keeper::shard()`. In Crafter, a source file of an item. |
| **Lore** (of a relic) | The first words of a `.rune`. | The first line: *"The Relic of Runite"* (older: *"The Artefact of Runite"*). Only a title — never read. |
| **Resonance** | What a runite reveals of itself. | `php <runite> --resonance` → `.echoes/<runite>/rune.json` (casts, runes, size, memory). |
| **Item** | A thing kept or crafted. | Keeper: a remembered value (JSON). Forger: a file. Crafter: what you build. |
| **Seed / spark** | The recipe, and the fire that builds it. | Crafter: `Crafter::seed(...)` sets DIST, TYPE, LANGUAGE…; `Crafter::spark('name')` bundles. → [Crafter](runes/crafter.md) |
| **Bond** | What Weaver remembers. | Values bound by `Weaver::bind()`, read with `Weaver::bond('name', null)`. |
| **Drain** | Silence. | `Whisper::drain(fn, true)` — catch output instead of printing it. |
| **Soul** | Memory that outlives a run. | Specter: `Specter::soul()` → `.echoes/<runite>/soul.json`. |
| **Seer** | Eyes beyond the flow. | Specter watching a cast or a folder. |
| **Familiar** | An AI spirit that answers. | Minister's config `.echoes/<runite>/familiar.json` (`url`, `token`, `model`). |

## Reading and guarding

| Word | Lore | In code |
|---|---|---|
| **Grimoire** | The book of every rune. | Built-in runite: `grimoire --runic=X`, `--runic-list`, `--arcane`, `--arcane-clean`, `--ai-adaptation`. → [grimoire](runites/grimoire.md) |
| **Arcane** | The trace of every step. | The run log: `aether_arcane()` → Keeper → `.echoes/<runite>/arcane.txt` (+ `arcanes/<date>.txt`). |
| **Glitch** | When the flow breaks. | An error or exception caught by Keeper → `.echoes/<runite>/glitch.txt` and the glitch screen. |
| **Sentinel** | The guard of a runite. | Built-in runite: `--gitignore`, unlock `--liberation` / `--federation`, `--runite-insert` / `--runite-remove` a rune, and in liberation: `--runic-create` / `--runic-delete`, `--phantasm-upgrade` / `--phantasm-repair`. → [sentinel](runites/sentinel.md) |
| **Awakening** | The first step into Rune. | Built-in runite: write the blank runite, or a relic of `devneet-id/reliquary`, as your runite. → [awakening](runites/awakening.md) |
| **Zero trust** | Trust nothing; leave no trace. | Spell `--zero-trust`: arcane off, output drained. |
| **Sentinel markers** | Where the guard writes. | `#sentinel-manifest` (the `use` lines), `#sentinel-awaken` (arise lines), `#sentinel-codex` (before the closing `end()` calls). |

## Spell words

Spells use **system words**; lore words stay in the names of runites and things.

| Shape | Means | Examples |
|---|---|---|
| `--<thing>` | look at one | `--runic`, `--shard`, `--relic` |
| `--<thing>-list` / plural | the list | `--runic-list`, `--shards`, `--relics` |
| `--<thing>-<action>` | do something to it | `--runic-create`, `--shard-remove`, `--phantasm-repair` |
| `--<from>-<to>` | move one into the other | `--runite-relic` (runite → relic), `--relic-runite` (relic → runite) |

A required spell is written in the cast `arg`, an optional one in its `echo`.

## Marks and signs

### Marks (Phantasm `mark`)
| Mark | Meaning |
|---|---|
| **VOID** | Empty — nothing. Two roles: a function held back because it is dangerous and returns nothing, or a function voided until its development is done. The default mark of `Rune\Phantasm`. |
| **BETA** | New and still settling. The default of a rune made by `runic-create`. |
| **EXIST** | The opposite of VOID: whole, stable, safe to use. |

A rune moves **VOID → BETA → EXIST**. There are only these three marks. DEVELOPMENT (still on Minister) and DEPRECATED (still named in the Grimoire header) are not marks — "development" means developing a *rune*.

### Arcane states — by the time of one step
| State | From |
|---|---|
| BURST | 0 s |
| FLASH | 0.0001 s |
| FLOW | 0.001 s |
| FALL | 2 s |
| BREAK | 5.5 s |
| COLLAPSE | 8.5 s |
| OVERCLOCK | 10 s |

### Symbols
| Sign | Meaning |
|---|---|
| `λ` | time |
| `ϟ` | stopwatch / stepwatch |
| `[ϻ]` | a Manifest call |
| `[ͱ]` | an Entity call |
| `◇Version=` | the version of Rune: `<major>.<minor + rune majors>.<rune minors>`, whole numbers; counted from the origin runes it is the release tag |
| `ϟExecute=` | run time |
| `ΞMemory=` | memory and peak |
| `[ᚱᚾ]` | a block in a `.rune` relic: `RELIC` (older: `ARTEFACT`), `RUNITE`, `ECHOES`, `SHARDS` |

### Whisper icons
`[√]` success · `[!]` warning · `[x]` danger / error / failed · `[i]` info · `[~]` primary · `[#]` secondary · `[^]` debug

## Template tokens

| Token | Filled by | Note |
|---|---|---|
| `{{nl}}` `{{tab}}` `{{bold}}` `{{end}}` `{{php}}` | Whisper | `{{php}}` = the PHP binary |
| `{{color-X}}` `{{text-X}}` `{{bg-X}}` `{{icon-X}}` `{{label-X}}` | Whisper | X = primary, secondary, success, warning, info, danger, error, failed, debug, default, end |
| `{{any-name}}` | `Weaver::bind($template, ['any-name' => …])` | lower or upper case, not mixed |
| `{{file}}` | Awakening | the runite name when it is written |
| `{{self}}` | Specter | `php <runite>` |

## Acts

An **Act** is a step of the user. Each Act limits the runes you use — its code never reaches into a later Act.

| Act | Runes | |
|---|---|---|
| 0 · The Void | Aether, Whisper, Weaver, Chanter | [→](acts/0-the-void/README.md) |
| 1 · First Resonance | the four in a CLI app, then + Forger, Cipher, Keeper · the relic | [→](acts/1-first-resonance/README.md) |
| 2 · Understanding Its Flow | all of Act 1 + Crafter, then Exura | [→](acts/2-understanding-its-flow/README.md) |
| 3 · Liberation of Forte | + Specter, Minister, then runes of your own · new apps | [→](acts/3-liberation-of-forte/README.md) |
| 4 · The Beyond | everything — maintain, release, contribute | [→](acts/4-the-beyond/README.md) |

## Old names

You may still meet these in old code or comments.

| Before | Now |
|---|---|
| `rune.php` (main file) | `cast` |
| `arise()` / `_arise()` / `_aether_end()` | `begin()` / `end()` |
| `@ethereal/`, `@liberations/`, `<repo>/@bindrune/` (user runes) | `@liberation/` |
| `@bindrune/` (built-in runites) | `@runite/` |
| artefact, `artefact` cast | relic, `reliquary` cast |
| `--invoke` / `--revoke` (sentinel) | `--runite-insert` / `--runite-remove` |
| `--invoke` / `--revoke` / `--inspect` (artefact) | `--runite-relic` / `--relic-runite` / `--runite-inspect` |
| `--create-rune` / `--remove-rune` | `--runic-create` / `--runic-delete` |
| `--phantasm-up` / `--phantasm-fix…` | `--phantasm-upgrade` / `--phantasm-repair` |
| `grimoire --rune` / `--rune-all` | `--runic` / `--runic-list` |
| *The Awaken from Void* | *The Awakening of Void* |
| Nirvana (CSS/JS/PHP) | Exura |
| `shards/` folder | `shard.json` + relic |
| `chipher()` | `cipher()` |
