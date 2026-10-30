# Traps

> Mistakes that are easy to make, and how to avoid them.

| You see | Because | Do |
|---|---|---|
| `Keeper::item()` returns `true` but nothing is saved | `Keeper::begin()` / `Keeper::end()` are missing (Sentinel does not add them) | Add `Keeper::begin()` after `Chanter::begin()` and `Keeper::end()` before `Aether::end()` |
| An empty list is not saved | `Keeper::item('x', [])` is read as *get* | Save `(object) $list` |
| A spell value is cut at a space | From code, casts are split by spaces | Use `%20`, or quotes on the command line |
| `--flag` gives `'1'`, a missing spell gives `false` | That is how spells are read | Check `!$v || $v === '1'` when a value is required |
| VS Code shows `cast` as Plain Text | No extension and no shebang | Start with `#!/usr/bin/env php` |
| `Class "Rune\X\Manifest" not found` | The rune is not there (or was revoked) | `sentinel --revoke=X`, or create the rune |
| `sentinel --phantasm-*` says *not eligible* | Not in liberation mode | Add `Rune\Ethereal::liberation();` after the autoload |
| A liberation rune is ignored | Its name is an origin rune name | Rename it |
| `Weaver::bond('x')` errors | The second argument is required | `Weaver::bond('x', null)` |
