# Laws

> The rules Rune keeps. Break them and the flow breaks.

<!-- status: draft · sources: rune README (Laws of the Rune), rune-dev/notes/rune-paradigm.md, rune-tasks.md (decisions), grimoire/ai.txt -->

These are not style tips. Every tool in Rune — Sentinel, Grimoire, the footer, artefacts — expects them. Keep them and the tools work for you.

## The runes
1. **One rune, one purpose.** A rune never does another rune's work. Need a different Weaver? Make a new rune with its own name (`MYWeaver`).
2. **Five subjects, five files.** `Ether.php`, `Essence.php`, `Entity.php`, `Manifest.php`, `Phantasm.php` in `Rune\<Name>\`.
3. **Prefixes carry the name.** Ether `KEEPER_*`, Essence `$KEEPER_*`, Entity `keeper_*()`. The main ether/essence/entity is the bare name (`KEEPER`, `$KEEPER`, `keeper()`).
4. **Entity holds the logic.** Entities may call entities of other runes (`keeper_item_get`, `cipher_hash`, `aether_arcane`) — that is how runes work together.
5. **Manifest only forwards.** Each method calls an entity, records `aether_arcane('Rune.manifest.name')`, and returns. No logic of its own.
6. **Who may use whom** (from `grimoire/ai.txt`):
   - Ether → Essence, Entity, Manifest
   - Essence → Entity, Manifest
   - Entity → Manifest, other Entities
   - Manifest → other Entities, other Manifests
7. **Never instance a core Manifest**; awaken before use (`X::ether()::essence()::entity()`).
8. **Aether flows everywhere.** Runes are not standalone packages. Depending on Aether is the design.

## The contract
9. **Every node has a `#NOTE`** on the line above it in the code — the Phantasm `node` list mirrors these notes (`sentinel --phantasm-fix-node`, `--phantasm-fix-note`).
10. **Every change raises the Phantasm version** of the rune that changed. See [Versioning](versioning.md).
11. **Marks are VOID, BETA, EXIST.** VOID = empty: held back because dangerous, or voided until done. BETA = being shaped. EXIST = the opposite of VOID: whole and stable. There is **no DEVELOPMENT and no DEPRECATED** mark; Minister still carries DEVELOPMENT.

## Liberation
12. **A liberation rune never replaces an origin rune.** The loader is appended, `--create-rune` refuses origin names, and Sentinel skips `@liberations/Whisper/` with a warning.
13. **One home for your runes: `@liberations/`.** Not `@ethereal/`, not `<repo>/@bindrune/`.

## Names and files
14. **Lore name = code name.** A new word goes into the [Glossary](../../glossary.md) first; the code uses the same word.
15. **A runite without `.php` starts with a shebang:** line 1 `#!/usr/bin/env php`, line 2 `<?php`. *(Rule decided; templates follow in T47.)*
16. **Echoes live in `.echoes/<runite>/`** — one folder per runite. Do not name your own items like the system files (`rune.json`, `soul.json`, `cast.json`, `shard.json`, `grimoire.json`).

## Working on Rune
17. **Files in `rune` are CRLF.** Keep them CRLF; `php -l` every changed PHP file.
18. **Notes live in `rune-dev`, never in `rune`.** The `rune` repo holds only what ships.
19. **Prove before you change.** A trial in `rune-dev/scenario` first, then the fix. See [The Workshop](the-workshop.md).
