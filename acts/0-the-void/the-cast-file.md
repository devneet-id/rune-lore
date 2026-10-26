# The Cast File

> A runite is one file. Its default name is `cast`.

<!-- status: draft -->

A runite is a rune that became a thing. It is one PHP file you run from the command line — your whole app begins there. Rune calls it `cast` by default, but any name works.

## The shebang
A file without `.php` must start with:
```
#!/usr/bin/env php
```
It tells the system — and your editor — that this is PHP. Without it some editors (VS Code among them) open `cast` as plain text. A file named `cast.php` does not need it.

## The whole runite, top to bottom
This is a complete runite with the four runes of this Act. It runs as it is.

```php
#!/usr/bin/env php
<?php                                                 // 1 shebang (alone on the first line) + PHP
require_once __DIR__ . '/vendor/autoload.php';       // 1 Composer autoload

use Rune\Aether\Manifest as Aether;                  // 2 manifest
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
#sentinel-manifest

Aether::ether()::essence()::entity();                // 3 awaken
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();                                     // 4 begin
Chanter::begin();

// 5 your casts live here

#sentinel-codex                                      // 6 codex
Chanter::end();                                      // 7 end
Aether::end();
```

| Part | What it does | Page |
|---|---|---|
| 1 · shebang and autoload | makes the file runnable; lets PHP find `Rune\…` | — |
| 2 · manifest | names the runes this runite will call | [Manifest](manifest.md) |
| 3 · awaken | loads each rune's Ether, Essence and Entity | [Awaken](awaken.md) |
| 4 · begin | opens the flow | [Begin and End](begin-and-end.md) |
| 5 · casts | your app: commands registered with `Chanter::cast()` | [Your First Runite](first-runite.md) |
| 6 · codex | a marker — the place right before the end | [Begin and End](begin-and-end.md) |
| 7 · end | runs the asked cast, then closes the flow with the footer | [Begin and End](begin-and-end.md) |

## The three markers
`#sentinel-manifest`, `#sentinel-awaken` and `#sentinel-codex` are plain comments. PHP ignores them; **Sentinel** uses them to write runes into your runite for you (Act 1). Keep them where they are.

## The runite knows itself
Two constants from Aether describe the runite while it runs:

| Constant | Value |
|---|---|
| `AETHER_FILE` | the runite as you typed it, e.g. `cast` |
| `AETHER_REPO` | the folder you ran it from |

Run a runite from its own folder. It matters more once it starts to remember, in Act 1.

Next: [Manifest](manifest.md)
