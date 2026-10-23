# The Workshop

> Never change Rune without testing it like a user.

<!-- status: draft · sources: rune-dev/notes/rune-dev-workflow.md, rune-dev/scenario/README.md, rune-dev/composer.json, rune-dev/control/ -->

Rune is tested the way it is used: through runites. The workshop is a second repo, `rune-dev`, that sits next to `rune` and loads it from disk. Every change is proved there before it is committed.

## The two folders
```
anwar-achilles/
├── rune/        the package — only what ships
└── rune-dev/    the workshop — runites, trials, notes, tools
```

`rune-dev/composer.json` maps `Rune\` to the local package:
```json
{ "autoload": { "psr-4": { "Rune\\": "../rune/" } } }
```
Run `composer dump-autoload` once (and again only when this file changes). Every runite in the workshop requires `rune-dev/vendor/autoload.php`, so it uses **your** copy of Rune, not Packagist.

## What lives in the workshop
| Folder | Use |
|---|---|
| `scenario/` | runites from easy to complex; each has a `test` cast (its **trial**) |
| `scenario/coverage/` | `trials` runs every trial · `coverage` counts the Phantasm nodes the scenarios touch |
| `control/` | maintainer runites: `cast` (Awakening) and `liberate` — a runite in **liberation mode**, used for `sentinel --phantasm-*` on the runes |
| `examples/` | small runites kept from past fixes (without Keeper, with Keeper, liberation, CRLF, Crafter…) |
| `tools/lore-runes/` | generates `rune-lore/runes/` — see [Keeping the Lore](keeping-the-lore.md) |
| `vscode-cast-test/` | why a `cast` needs a shebang (T47) |
| `notes/` | tasks, decisions, commit and release notes — **never** in `rune` |

## Run the trials
Run each runite **from its own folder** (Rune uses `getcwd()`).
```bash
cd rune-dev/scenario/01-greeting
php cast test                 # the trial of one scenario

cd ../coverage
php cast trials               # every trial at once
php cast coverage             # nodes touched per rune
php cast coverage --rune=Keeper
```
A trial counts checks (`trial('label', $condition)`); a glitch fails one check instead of ending the run. Trials back up and restore their own data. Helpers are in `scenario/trial.php`: `trial`, `trial_cast`, `trial_capture`, `trial_safe`, `trial_section`, `trial_report`.

Today: **105/113** checks pass; the 8 failures are [Known Issues](known-issues.md). Coverage is **56/298 nodes (19%)** — Crafter, Specter, Minister and most ether/essence nodes have no scenario yet.

## Work on a rune
```bash
cd rune-dev/control
php liberate                                  # "The Liberation of Forte" on the main screen
php liberate grimoire --rune=Weaver           # read the contract
php liberate sentinel --phantasm-fix=Weaver   # node + link + note + version
php liberate sentinel --phantasm-up=Weaver    # only raise the version
```
`--phantasm-*` spells are refused outside liberation mode ("You are not eligible!!").

## Test the released version
To check what users get, make a separate folder with its own `composer.json` and `composer require devneet/rune`. The same runite runs unchanged — only the autoload source differs.

## Rules of the bench
- Files in `rune` are **CRLF**: edit by bytes, check `grep -c $'\r'` before and after, `php -l` every PHP file.
- A new scenario: a folder, a `cast` with the shebang, `require_once __DIR__ . '/../../vendor/autoload.php';`, a `test` cast.
- A fix without a trial is a guess. Add the check first, watch it fail, then fix.
