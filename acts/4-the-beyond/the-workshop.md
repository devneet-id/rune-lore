# The Workshop

> Never change Rune without testing it like a user.

<!-- status: draft -->

Rune is tested the way it is used: through runites. Keep a **workshop** — a folder of your own, next to your clone of `rune`, that loads Rune from disk. Every change is proved there before it is committed. The workshop is yours; it is not part of any repo.

## Set it up
```
your-folder/
├── rune/        your clone or fork of devneet-id/rune — only what ships
└── workshop/    your runites and trials (any name)
```

`workshop/composer.json` maps `Rune\` to the local package:
```json
{ "autoload": { "psr-4": { "Rune\\": "../rune/" } } }
```
Run `composer dump-autoload` once (and again only when this file changes). Every runite in the workshop requires `workshop/vendor/autoload.php`, so it uses **your** copy of Rune, not Packagist.

## What to keep in it
| Folder | Use |
|---|---|
| `scenario/` | runites from easy to complex, one folder each; every runite has a `test` cast — its **trial** |
| a runner | one runite that runs every trial, and (if you like) counts which Phantasm nodes the scenarios touch |
| a liberation runite | `Rune\Ethereal::liberation();` — for `sentinel --phantasm-*` on the runes you change |

## Write a trial
A trial is a cast that checks, not prints. A tiny helper is enough:
```php
function trial( $label, $ok ) {
  global $TRIAL; $TRIAL[] = $ok;
  Whisper::echo(($ok ? '{{color-success}} ✓ ' : '{{color-danger}} ✗ ') . '{{color-end}}' . $label . '{{nl}}');
}

Chanter::cast('test', function() {
  trial('greet answers', Chanter::cast('greet --name=Rune')() === 'Hello, Rune');
  // …one line per behaviour
}, 'Run the trial of this runite.');
```
- Catch PHP warnings as errors (`set_error_handler` → `ErrorException`) so a glitch fails one check instead of ending the run.
- Back up and restore any data the trial touches.
- Run each runite **from its own folder** — Rune uses `getcwd()`.

```bash
cd workshop/scenario/01-greeting
php cast test
```

## Work on a rune
```bash
php liberate                                  # "The Liberation of Forte" on the main screen
php liberate grimoire --rune=Weaver           # read the contract
php liberate sentinel --phantasm-fix=Weaver   # node + link + note + version
php liberate sentinel --phantasm-up=Weaver    # only raise the version
```
`--phantasm-*` spells are refused outside liberation mode ("You are not eligible!!").

## Test the released version
To check what users get, make another folder with its own `composer.json` and `composer require devneet/rune`. The same runite runs unchanged — only the autoload source differs.

## Rules of the bench
- Files in `rune` are **CRLF**: keep the line endings, and `php -l` every PHP file you touch.
- A new scenario: a folder, a `cast` with the shebang, the workshop autoload, a `test` cast.
- A fix without a trial is a guess. Add the check first, watch it fail, then fix.
- Notes, drafts and trials stay in the workshop — never in `rune`.
