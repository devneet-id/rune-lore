# Whisper

> Whisper is the voice of the runite. Everything the user reads — and every question the app asks — passes through it.

<!-- status: draft · sources: runes/whisper.md -->

→ Reference: [Whisper](../../runes/whisper.md)

## Speak
`Whisper::echo()` prints a line with **tokens**:

```php
Whisper::echo('{{color-success}}{{icon-success}} Added #1{{nl}}');
Whisper::echo('{{color-warning}}{{icon-warning}} Removed #2{{nl}}');
Whisper::echo('{{color-danger}}{{icon-danger}} No note #5{{nl}}');
```
```
[√] Added #1
[!] Removed #2
[x] No note #5
```

- `{{color-X}}` colors the text, `{{icon-X}}` adds the icon, `{{nl}}` ends the line.
- X = `primary`, `secondary`, `success`, `warning`, `info`, `danger`, `error`, `failed`, `debug`…
- Whisper closes the color for you at the end of every echo.

The app uses one color per meaning: success for done, warning for removed, danger for "not found", secondary for quiet hints.

## Ask
`Whisper::call()` asks and waits for one line:

```php
if ($text === '1') $text = Whisper::call('Note: ');
```
```
$ php cast note --add
>>> Note: Water the plants
[√] Added #1
```

The `>>>` is Whisper's own. The answer comes back trimmed.

## Stay silent
`Whisper::drain()` runs something and **catches** its output instead of printing it:

```php
$out = Whisper::drain(fn() => Chanter::cast('notes')());
// $out holds the list as text; nothing was printed
```

Use it to test a cast, or to build a bigger text from smaller ones. `--zero-trust` does the same for a whole cast.

Next: [Weaver](weaver.md).
