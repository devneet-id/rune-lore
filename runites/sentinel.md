# Sentinel

> Someone or something that guards.

Sentinel guards your runite. It writes runes into it and takes them out, and — in liberation mode — helps you shape runes of your own.

## Spells
| Spell | Does |
|---|---|
| `sentinel --invoke=Keeper` | adds `use Rune\Keeper\Manifest as Keeper;` and `Keeper::ether()::essence()::entity();` at the markers |
| `sentinel --invoke=Keeper.entity` | awakens only some parts (`ether`, `essence`, `entity`) |
| `sentinel --revoke=Keeper` | removes them again (`Keeper.essence` removes one part) |
| `sentinel --altar` | starts Altar, the GUI (in development) |

### Liberation only
| Spell | Does |
|---|---|
| `sentinel --create-rune=ledger` | creates `@liberations/Ledger/` with the five files (origin names are refused) |
| `sentinel --remove-rune=Ledger` | removes it and revokes it from the runite |
| `sentinel --phantasm-fix-node=Ledger` | rebuilds the node list from the code |
| `sentinel --phantasm-fix-note=Ledger` | copies every `#NOTE` into the nodes |
| `sentinel --phantasm-fix-link=Ledger` | finds which runes it uses |
| `sentinel --phantasm-fix-link-all` | links for every rune |
| `sentinel --phantasm-up=Ledger` | raises its minor version by one (`0.9` → `0.10`); refuses an unknown rune or a version that is not `<major>.<minor>` |
| `sentinel --phantasm-fix=Ledger` | node + link + note at once, then raises the version only if one of them changed |

## Notes
- Sentinel writes at `#sentinel-manifest` and `#sentinel-awaken`. Keep the markers.
- `--invoke=Keeper` does not add `Keeper::begin()` / `Keeper::end()` — write them yourself.
- Sentinel keeps the runite's own line ending (CRLF or LF).
- Rune names are written as `Ucfirst` (`ledger` → `Ledger`).
