# Awaken

> A called rune still sleeps. Awaken it.

<!-- status: draft · sources: Rune/Manifest.php, rune-lore.md (Arise / awaken), tested in rune-dev -->

Naming a rune is not enough. A rune sleeps until its truth, its flow and its will are woken — in that order.

## In code
```php
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
#sentinel-awaken
```

Each call loads one file of the rune and returns the Manifest again, so the three can be chained:

| Call | Loads | Wakes |
|---|---|---|
| `ether()` | `Ether.php` | the constants |
| `essence()` | `Essence.php` | the globals |
| `entity()` | `Entity.php` | the functions |

Ether first, because Essence and Entity may read its constants. Essence next, because the Entity reads its globals. Entity last.

## Aether first
Every rune leans on Aether, so awaken Aether first. Keep the order of the template: Aether, Whisper, Weaver, Chanter.

## When a rune sleeps
Call a rune you have not awakened and PHP stops at once:

```php
use Rune\Whisper\Manifest as Whisper;
Whisper::echo('hi{{nl}}');      // not awakened
```
```
PHP Fatal error:  Uncaught Error: Call to undefined function Rune\Whisper\whisper_echo_set()
```

A rune can also need another rune awake. Whisper fills its `{{tokens}}` with Weaver, so Whisper without Weaver fails the same way:

```
PHP Fatal error:  Uncaught Error: Call to undefined function weaver_bind_multiple()
```

The Phantasm says this in its `link`: Whisper links Aether and Weaver. In this Act, always awaken all four.

## The marker
`#sentinel-awaken` closes the awaken lines. Sentinel writes new ones above it.

## Old name
Older code and comments call this **arise**. It is the same thing.

Next: [Begin and End](begin-and-end.md)
