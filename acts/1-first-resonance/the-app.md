# The App

> One app for the whole Act: a small CRUD of notes.

An app in Rune is a runite. Before you engrave, plan its casts and spells — they are the app's whole surface.

## What it does
| Action | Cast |
|---|---|
| **C**reate | `php cast note --add="Buy milk"` |
| **R**ead | `php cast notes` |
| **U**pdate | `php cast note --edit=1 --text="Buy oat milk"` |
| **D**elete | `php cast note --remove=1` |

`php cast note` with no spell shows the list.

## The runes it needs — for now
Only the four from Act 0:

| Rune | Job in the app |
|---|---|
| [Chanter](chanter.md) | the casts and spells |
| [Whisper](whisper.md) | what the app says and asks |
| [Weaver](weaver.md) | the shape of one row of the list |
| [Aether](aether.md) | the flow: time and debug |

## The folder
```
notes/
├── cast              the runite
├── vendor/           Rune (Composer)
└── weaver/
    └── row.txt       the template of one row (from the Weaver page)
```

## The skeleton
Start from the Blank Starter. Keep the three markers — Sentinel writes at them in Part II.

```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
#sentinel-manifest
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();
Chanter::begin();

// the notes live in memory only — for this run
$NOTES = [];

// casts go here

#sentinel-codex
Chanter::end();
Aether::end();
```

`$NOTES` is a plain PHP array. Hold that thought — [It Forgets](it-forgets.md) comes back to it.

Next: [Chanter](chanter.md).
