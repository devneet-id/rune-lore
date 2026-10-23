# Manifest

> Call a rune into your runite by its Manifest.

<!-- status: draft · sources: rune-paradigm.md §4, Rune/Whisper/Manifest.php, runites/sentinel.md -->

The Manifest is the face a rune shows to the world. Your runite never reaches into a rune's heart; it speaks to its face, and the face carries the words inside.

## In code
```php
use Rune\Whisper\Manifest as Whisper;
#sentinel-manifest
```
`Rune\Whisper\Manifest` is a static class. The `as Whisper` gives it the rune's name, so the rest of your runite reads like the lore:

```php
Whisper::echo('Hello{{nl}}');
```

## Why the Manifest
- **It is the door for runites.** Manifest methods are made to be called from your engraving.
- **It holds no logic.** Each method forwards to the rune's Entity, leaves a trace for Aether, and returns. `Whisper::echo()` forwards to `whisper_echo_set()`.
- **It stays static.** You never write `new Whisper()`. A rune is not an object you make; it is a power you call.

## Only what you call exists
A `use` line only gives a name. Nothing loads until the rune is awakened (next page), and a rune you never name is never touched. That is why Rune stays light: a runite carries only the runes it needs.

## The marker
`#sentinel-manifest` closes the list of `use` lines. When you later ask Sentinel to bring a rune in, it writes the new `use` line right above this marker. Keep it.

## Origin runes in this Act
```php
use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
```
Every method of every Manifest is listed in [Runes](../../runes/README.md).

Next: [Awaken](awaken.md)
