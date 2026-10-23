# Contributing

> From an issue to a merged change.

<!-- status: draft · sources: rune CONTRIBUTING.md, rune-dev/notes/rune-pr.md, rune-tasks.md (way of working), rune README (laws) -->

Anyone who keeps the laws can keep Rune. You do not need its first creator — you need a trial that proves the problem, a change that keeps the contract, and a clear pull request.

## 1. Set up
- PHP 8.1 or newer, Composer, Git.
- Fork `devneet-id/rune`, clone it next to a workshop folder:
```
your-folder/
├── rune/        your fork
└── rune-dev/    composer.json → "Rune\\": "../rune/"
```
- `composer dump-autoload` in `rune-dev`. Make one normal runite (Awakening) and one in liberation mode (`Rune\Ethereal::liberation();`) — see [The Workshop](the-workshop.md).

## 2. Find the work
- [Known Issues](known-issues.md) — bugs with their files.
- A failing trial in `rune-dev/scenario`.
- A Phantasm that no longer matches the code (`grimoire --rune=X` vs the source).
- An issue on GitHub. Open one if none exists: what you ran, what you saw, what you expected.

## 3. Prove it
Write the check before the fix: a `trial(...)` in an existing scenario, or a new scenario folder with its own `test` cast. Run it and watch it fail.

## 4. Change it — keep the laws
- Logic goes into **Entity**; the **Manifest** only forwards and records arcane.
- A `#NOTE` above every new node.
- New constants, globals, functions use the rune prefix.
- Do not stretch a rune into another rune's purpose.
- Keep CRLF; `php -l`.

The upstream `CONTRIBUTING.md` shows a handy way to build a new node: write its Ether, Essence, Entity and a small Manifest inside a test cast first, run it, then move each part into the right file of the rune.

## 5. Update the contract
From your liberation runite:
```bash
php liberate sentinel --phantasm-fix-node=Whisper    # nodes from the code
php liberate sentinel --phantasm-fix-note=Whisper    # #NOTE → nodes
php liberate sentinel --phantasm-fix-link=Whisper    # runes it uses
php liberate sentinel --phantasm-up=Whisper          # raise the version
php liberate grimoire --rune=Whisper                 # read it back
```
`--phantasm-fix=Whisper` runs node + link + note + version at once.

## 6. Test again
Your trial passes, and nothing else broke: `php cast trials` in `scenario/coverage`.

## 7. Pull request
- Branch from `1.x`, one commit per change ([Release](release.md) has the commit format).
- Title: like a commit (`fix: ...`, `fix(sentinel): ...`).
- Description:
```markdown
## Summary
What changes, in two sentences.

## Commits
- fix(chanter): ... (issue/task)

## Why
| # | Problem |
|---|---|

## Test
- php cast test in scenario/... → n/n
- php cast trials → n/n
```
- Include the trial (or the test cast) so the reviewer can run it.

## A new origin rune?
New runes start as **liberation runes** in `@liberations/` ([Create a Rune](../3-liberation-of-forte/create-rune.md)). An origin rune is added only when a liberation rune has proved a purpose no origin rune has. Propose it in an issue first, with its Phantasm and its runites.

## Contributing to the lore
Changed behaviour → change the lore in the same round. See [Keeping the Lore](keeping-the-lore.md).
