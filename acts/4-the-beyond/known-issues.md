# Known Issues

> What is still open — and where to start.

Rune is not finished. These are the issues found by the trials and by reading the code. Each one names the file, so you can start right away. Pick one, write its trial, fix it — see [Contributing](contributing.md).

## Bugs
| Issue | Where | What happens |
|---|---|---|
| `chanter_cast_has()` is always `false` | `Chanter/Entity.php` | It reads `$CHANTER_CAST` without `global $CHANTER_CAST`. |
| `Keeper::echo()` cannot write | `Keeper/Entity.php` · `keeper_echo_set()` | It passes one path map to `forger_fix()`, which expects a list → glitch. Reading works. |
| `weaver_item($file, [...])` with data glitches | `Weaver/Entity.php` · `weaver_item()` | It calls `weaver_bind()` instead of `weaver_bind_multiple()` → "Array to string conversion". Bind the result with `Weaver::bind()` meanwhile. |
| An artefact with exactly one shard breaks | `@bindrune/chanter/artefact/cast.php` · the parser | A block with one line is read as a string: `--inspect` glitches, `--revoke` says *success* but does not write the shard. Carry none, or two and more. |
| `grimoire --rune=<unknown>` | `@bindrune/chanter/grimoire/cast.php` | Fatal error (class not found) instead of a message. |
| Exura templates on Linux | `@bindrune/awakening/src/*Exura*.rune` | Shards are stored with Windows paths (`src/exura/\exura.*`); revoking them on Linux writes odd file names. |

## Sentinel
| Issue | What happens |
|---|---|
| `--invoke=Keeper` adds no `begin()`/`end()` | Without `Keeper::begin()` nothing is saved, yet `Keeper::item()` returns `true`. Add them by hand. |
| Names are `ucfirst(strtolower())` | `MYWhisper` becomes `Mywhisper` (the name `--create-rune` itself suggests). |
| `--revoke` does not validate the rune name | Unknown names are not refused like in `--invoke`. |

## Contract and text
- Some `#NOTE`s are inaccurate: Keeper `begin`/`end`, generic `end()`, "placeholder" for `cipher()` / `forger()`. Fix the `#NOTE`, then `--phantasm-fix-note`.
- `_arise()` hooks remain in the Manifests of Cipher, Forger, Specter, Weaver and Whisper — never called (legacy).
- Minister still has the mark `DEVELOPMENT`, which is not a mark (should be VOID, BETA or EXIST).
- The Grimoire header still says *Carefull use rune BETA/DEPRECATED* (`@bindrune/chanter/grimoire/header.txt`); DEPRECATED is not a mark.
- `composer.json` `support` links point to `github.com/devneet/rune`; the repo is `devneet-id/rune`.
- Awakening template headers use old Act labels ("Act. 1 – Understanding Its Flow", "Act. 3", "THE BEYOND Act. 1") — to align with the [Acts](../../README.md).

## Planned work
| Task | State | Plan |
|---|---|---|
| Altar → Exura | postponed | Altar still uses Nirvana, runs `start cmd /k` (Windows only) with unsanitised POST input, and old paths (`.echoes/rune.php/`, `shards/`). See [Altar](altar.md). |

## Not tested yet
- Specter on macOS (Terminal via `osascript`) — written, never run on a Mac.
- Minister against a real familiar (URL + token).
- Windows-only paths (`cls`, `start cmd`) are written by `PHP_OS_FAMILY`; the trials run on Linux.
