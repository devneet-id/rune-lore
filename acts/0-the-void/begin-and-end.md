# Begin and End

> Aether opens the flow first and closes it last.

<!-- status: draft · sources: Rune/Aether/Manifest.php, Rune/Chanter/Manifest.php, aether_exit(), tested in rune-dev -->

Every run of a runite is one flow. It has a beginning and an end, and what opens first closes last — like a spell that must be sealed in the reverse order it was cast.

## In code
```php
Aether::begin();
Chanter::begin();

// your casts

#sentinel-codex
Chanter::end();
Aether::end();
```

## What each step does
| Step | What happens |
|---|---|
| `Aether::begin()` | the flow opens: memory is tidied and the trace of this run starts fresh |
| `Chanter::begin()` | the built-in casts are loaded from `@bindrune/chanter/` — `rune`, `grimoire`, `artefact`, `sentinel` |
| your casts | `Chanter::cast('greet', fn, …)` **registers** a cast. Nothing runs yet. |
| `Chanter::end()` | reads the command line and runs the cast you asked for |
| `Aether::end()` | prints the footer and **exits** |

So a cast is only a promise until `Chanter::end()`. And `Aether::end()` is truly the end: no line after it runs.

### Which cast runs
| You type | Chanter runs |
|---|---|
| `php cast` | `rune` — the main screen |
| `php cast greet` | your cast `greet` |
| `php cast --name=x` (only spells) | `rune` with those spells |
| `php cast gret` | no such cast: `[!]WARNING: Chanter cast with 'gret' not found.` then `[i]INFO: You mean: greet,` |

## Forget one, and see
| Forgotten | What you see |
|---|---|
| `Chanter::end()` | only the footer — your cast never runs, and no error tells you |
| `Aether::end()` | the cast runs, but no footer |
| `Aether::begin()` | it still runs today, but the trace of the run is not reset — always write it |

## The codex marker
`#sentinel-codex` marks the place right before the closing calls. Later runes that also open and close (Keeper, in Act 1) close here too, in reverse order.

## The footer
Every run ends with one line:
```
◇Version=1.12.31: ϟExecute=0.0040s, ΞMemory=926.73KB - ^1.10MB
```
| Sign | Meaning |
|---|---|
| `◇Version=` | `1.` + the sum of the Phantasm versions of every rune |
| `ϟExecute=` | how long the run took |
| `ΞMemory=` | memory used, and `^` the peak |

The version grows every time a rune changes, so the footer tells you which Rune you are running. More in [the main screen](../../runites/rune.md#the-footer).

## Old names
Older code and comments use `arise()`, `_arise()` and `_aether_end()`. Today they are `begin()` and `end()`.

Next: [Install](install.md)
