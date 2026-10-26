# Specter

> Work beyond the main flow.

A flow begins, does its work and ends. Specter is what stays when it ends — a **soul** that outlives the run — and what moves beside it: a cast in another window, a **seer** that keeps watching, a server that keeps serving.

Specter keeps its memory in `.echoes`, so **Keeper must be engraved** (with `Keeper::begin()` and `Keeper::end()`).

## Engrave it
```bash
php cast sentinel --invoke=Specter
```
Then check that `Keeper::begin()` / `Keeper::end()` are in your runite ([Sentinel](../1-first-resonance/sentinel.md)).

## Soul — memory that outlives a run
```php
Chanter::cast('mood --set', function() {
  $set = Chanter::spell('set');
  if ($set && $set !== '1') Specter::soul('mood', $set);
  Whisper::echo('mood = ' . (Specter::soul('mood') ?: '(empty)') . '{{nl}}');
}, 'A soul outlives the run. --set=calm');
```
```
$ php cast mood --set=calm
mood = calm
$ php cast mood
mood = calm
```
The soul lives in `.echoes/<runite>/soul.json`:
```json
{
  "mood": "calm"
}
```
- `Specter::soul('name')` returns the value, or `false` when it is not there.
- An empty value (`''`, `0`, `'0'`) is not written — `Specter::soul('x', 0)` only reads.

## Cast — beside the flow
`Specter::cast()` runs a command outside this flow. `{{self}}` becomes `php <runite>`.
```php
Chanter::cast('stamp', function() {
  Forger::item(__DIR__ . '/stamp.txt', date('H:i:s'));
}, 'Write the time into stamp.txt.');

Chanter::cast('behind', function() {
  Specter::cast('{{self}} stamp', ['visible' => false]);
  Whisper::echo("stamp is being written behind this flow{{nl}}");
}, 'Run the stamp cast beside this flow, hidden.');
```
The options, with their defaults:

| Option | Default | Means |
|---|---|---|
| `visible` | `true` | open a new terminal window (`cmd` on Windows, Terminal on macOS, `gnome-terminal` on Linux) |
| `blocking` | `false` | wait until the command ends |
| `exit` | `true` | close the window when the command ends |
| `title` | `SPECTER_CAST` | the window title |

Specter writes what it casts into `.echoes/<runite>/cast.json` (`alive: true` while it is cast). `Specter::exit('{{self}} stamp')` marks it as no longer alive.

## Seer — a loop that watches
The seer calls your function again and again (every 100 ms) with a spinner frame, until it returns `true` or a glitch happens.
```php
Chanter::cast('count', function() {
  $n = 0;
  Specter::seer(function($frame) use (&$n) {
    Whisper::echo("\r$frame " . ++$n);
    return $n >= 5;
  });
  Whisper::echo("{{nl}}done{{nl}}");
}, 'The seer loops until the callback returns true.');
```

`Specter::observer($folder, fn)` is a seer that calls `fn` each time a file in `$folder` changes. It runs until **Ctrl+C**.

## Dev server
```php
Chanter::cast('serve', function() {
  Specter::devserver(['port' => 8000, 'path' => __DIR__ . '/public']);
}, 'Serve ./public on http://127.0.0.1:8000');
```
`host` (default `127.0.0.1`), `port` (`8000`), `path` (document root), `file` (a router file), `mode` (`public` listens on `0.0.0.0`). It runs until **Ctrl+C**. A good pair with a [bundle](../2-understanding-its-flow/bundling.md): build with Crafter, serve with Specter.

## Remember
- No Keeper, no soul: Specter writes everything in `.echoes/<runite>/`.
- Run the runite from its own folder ([why](nested-runites.md)).

→ Reference: [runes/specter.md](../../runes/specter.md)
