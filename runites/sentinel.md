# Sentinel

> Someone or something that guards.

Sentinel guards your runite. It unlocks the modes, writes runes into the runite and takes them out, and — in liberation mode — helps you shape runes of your own.

## Spells
| Group | Spell | Does |
|---|---|---|
| HELP | `sentinel --gitignore` | writes a marked block in the `.gitignore` next to the runite: `vendor/` and every `.echoes/` |
| UNLOCK | `sentinel --liberation` | writes `Rune\Ethereal::liberation();` under the `require` line, opens `@liberation/` |
| UNLOCK | `sentinel --federation` | writes `Rune\Ethereal::federation();` under the `require` line, opens `@federation/` |
| RUNITE | `sentinel --runite-insert=Keeper` | adds `use Rune\Keeper\Manifest as Keeper;` and `Keeper::ether()::essence()::entity();` at the markers |
| RUNITE | `sentinel --runite-insert=Keeper.entity` | awakens only some parts (`ether`, `essence`, `entity`) |
| RUNITE | `sentinel --runite-remove=Keeper` | removes them again (`Keeper.essence` removes one part) |

### LIBERATION (liberation mode only)
| Spell | Does |
|---|---|
| `sentinel --runic-create=Ledger` | creates `@liberation/Ledger/` with the five files (origin names are refused) |
| `sentinel --runic-delete=Ledger` | deletes it and removes it from the runite |
| `sentinel --phantasm-upgrade=Ledger` | raises its minor version by one (`0.9` → `0.10`); refuses an unknown rune or a version that is not `<major>.<minor>` |
| `sentinel --phantasm-repair=Ledger` | node + link + note at once, then raises the version only if one of them changed |
| `sentinel --phantasm-repair=Ledger --mode=node` | only rebuilds the node list from the code (`--mode=note` copies every `#NOTE`, `--mode=link` finds which runes it uses) |
| `sentinel --phantasm-repair --all` | every rune (with or without `--mode`) |

The `.gitignore` block, written again (not added twice) on every run; your own lines are kept:
```
# rune (sentinel)
vendor/
.echoes/
# /rune
```

## Old spells
| Was | Is |
|---|---|
| `--invoke` / `--revoke` | `--runite-insert` / `--runite-remove` |
| `--create-rune` / `--remove-rune` | `--runic-create` / `--runic-delete` |
| `--phantasm-up` | `--phantasm-upgrade` |
| `--phantasm-fix`, `-node`, `-note`, `-link`, `-link-all` | `--phantasm-repair` (`--mode=…`, `--all`) |

## Notes
- An unlocked mode is not unlocked twice: Sentinel only tells you. To close a mode, delete its line by hand.
- Sentinel writes at `#sentinel-manifest` and `#sentinel-awaken`. Keep the markers.
- `--runite-insert=Keeper` does not add `Keeper::begin()` / `Keeper::end()` — write them yourself.
- Sentinel keeps the runite's own line ending (CRLF or LF).
- Rune names are matched whatever their case (`ledger` → `Ledger`).
- `--altar` (the GUI) and `--inspect` are still there, hidden while in development.
