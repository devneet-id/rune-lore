# Every Repo Is a Runite

> Rune manages Rune. Any repo can do the same.

<!-- status: draft -->

Look back at how Rune is kept. It is tested by runites. Its contract is fixed by a runite (Sentinel). Its version is counted by a runite (the footer). Its documentation is read by a runite (Grimoire). Rune is a simple tool that uses itself to grow — a fractal: runes inside runites, runites inside repos, repos made of runites.

## Rune keeps Rune
| Job | Done by |
|---|---|
| test every change | a `test` cast in every scenario runite ([The Workshop](the-workshop.md)) |
| measure what is tested | a runite that counts the Phantasm nodes the trials touch |
| keep each contract true | `sentinel --phantasm-fix` (from a liberation runite) |
| version the whole | `sentinel --phantasm-up` + the footer `Version=` |
| read the docs | `grimoire --rune-all` |
| pack and share | `artefact --invoke` |

None of this is a separate tool. Each one is a runite made of the same runes you use.

## Your repo can do the same
Any repo — a website, a library, a set of scripts — can carry its own runite, with casts that manage that repo:
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
use Rune\Forger\Manifest as Forger;
#sentinel-manifest
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
Forger::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();
Chanter::begin();

Chanter::cast('clean', function() {
  Forger::clean(__DIR__ . '/dist', true);
  Whisper::echo('{{color-success}}{{icon-success}} dist cleaned{{nl}}');
}, 'Remove the build folder.');

#sentinel-codex
Chanter::end();
Aether::end();
```
- Build with Crafter, serve with Specter, remember with Keeper, ship with an artefact.
- A derived repo grows its own runite app — with its own casts — that manages that repo.
- In liberation mode the repo can grow its own runes in `@liberations/`.

## The shape of it
```
rune (origin runes)
 └── a runite      — keeps rune itself
      └── your repo
           └── its runite   — keeps your repo
                └── its runes (@liberations/)
                     └── …
```
Each level uses the same five subjects and the same laws. That is the whole point of [Liberation](../3-liberation-of-forte/liberation.md): only the paradigm stays; everything else is yours.
