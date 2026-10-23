# Known Issues

> What is still open — and where to start.

<!-- status: draft · sources: rune-dev/scenario/README.md (trials), rune-tasks.md (T25, T47, T48), rune code (checked 2026-10-23) -->

Rune is not finished. These are the issues found by the trials and by reading the code. Each one names the file, so you can start right away. Pick one, write its trial, fix it — see [Contributing](contributing.md).

## Bugs
| Issue | Where | What happens |
|---|---|---|
| `chanter_cast_has()` is always `false` | `Chanter/Entity.php` | It reads `$CHANTER_CAST` without `global $CHANTER_CAST`. |
| `Keeper::echo()` cannot write | `Keeper/Entity.php` · `keeper_echo_set()` | It passes one path map to `forger_fix()`, which expects a list → glitch. Reading works. |
| `weaver_item($file, [...])` with data glitches | `Weaver/Entity.php` · `weaver_item()` | It calls `weaver_bind()` instead of `weaver_bind_multiple()` → "Array to string conversion". Bind the result with `Weaver::bind()` meanwhile. |
| Glitch screen labels swapped | `Keeper/Entity.php` · `keeper_glitch_message()` | *On Line Number* shows the file; *File Location* shows the line. |
| `.echoes` follows the current folder | `Aether/Ether.php`, `Keeper/Ether.php` | `KEEPER_ECHOES = getcwd() . '/.echoes/' . PHP_SELF`. `php realm/cast` from the parent writes `.echoes/realm/cast/`; inside `realm/` it writes `realm/.echoes/cast/` → two memories. **T48**, see below. |

## Sentinel
| Issue | What happens |
|---|---|
| `--invoke=Keeper` adds no `begin()`/`end()` | Without `Keeper::begin()` nothing is saved, yet `Keeper::item()` returns `true`. Add them by hand. |
| Names are `ucfirst(strtolower())` | `MYWhisper` becomes `Mywhisper` (the name `--create-rune` itself suggests). |
| `--revoke` does not validate the rune name | Unknown names are not refused like in `--invoke`. |
| `--phantasm-up=<unknown>` | Fatal error (class not found) instead of a message. |

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
| **T47** shebang in every template | decided, not done | Every `cast` without `.php` starts with `#!/usr/bin/env php`; re-encode the Awakening `.rune` templates, keep it through artefact and Sentinel round trips. |
| **T48** `.echoes` next to its runite | noted, needs a choice | (1) Keeper only: echoes from `dirname(realpath(SCRIPT_FILENAME))`; or (2) `AETHER_REPO` = runite folder, `AETHER_FILE` = name only (wider effect). Test: `scenario/07-nested` 11/11 from any folder. |
| **T25** Altar → Exura | postponed | Altar still uses Nirvana, runs `start cmd /k` (Windows only) with unsanitised POST input, and old paths (`.echoes/rune.php/`, `shards/`). See [Altar](altar.md). |
| Float versions | open decision | `1.10` counts as `1.1`. See [Versioning](versioning.md). |

## Not tested yet
- Specter on macOS (Terminal via `osascript`) — written, never run on a Mac.
- Minister against a real familiar (URL + token).
- Windows-only paths (`cls`, `start cmd`) are written by `PHP_OS_FAMILY`; the trials run on Linux.
