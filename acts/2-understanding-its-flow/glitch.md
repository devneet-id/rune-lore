# Glitch

> When the flow breaks, Keeper catches it.

A runite does not fall silently. When something breaks — an exception, a PHP warning, a fatal error — Keeper stops the flow, shows the **glitch** screen and writes it down in the echoes.

## Who catches it

`Keeper::begin()` calls `keeper_glitch_boot()`. From that moment Keeper holds three nets:

| Net | Catches |
|---|---|
| `set_error_handler` | errors, warnings, notices — **every** level (`error_reporting(E_ALL)`) |
| `set_exception_handler` | uncaught exceptions |
| `register_shutdown_function` | fatal and parse errors |

It also turns off PHP's own error printing (`display_errors = 0`), so the glitch screen is the only voice.

Without Keeper there is no net: PHP prints its usual error.

## The glitch screen

```php
Chanter::cast('break', function() {
  throw new Exception('The seal is broken.');
}, 'Break the flow on purpose.');
```

```
$ php cast break
///////////////////////////////////
 G L I T C H [!]
 Trouble need to fixing !!

 #  M A I N
 ♦ Severity:
    » EXCEPTION
 ♦ On Line Number:
    » 33
 ♦ File Location:
    » /home/you/app/cast
 ♦ Message:
    » The seal is broken.

 #  T R A C E

◇Version=1.20.110: ϟExecute=0.0095s, ΞMemory=1.09MB - ^1.27MB
```

A warning is a glitch too — and it stops the flow just the same. Errors also carry a **trace**: the path the flow took to get there.

```php
Chanter::cast('warn', function() {
  $list = [];
  return $list['missing'];
}, 'A PHP warning is a glitch too.');
```

```
$ php cast warn
 ♦ Severity:
    » ERROR
 ...
 ♦ Message:
    » Undefined array key "missing"

 #  T R A C E
 ♦ /home/you/app/cast [38]
 ♦ /home/you/app/vendor/devneet/rune/Chanter/Manifest.php [55]
 ♦ /home/you/app/cast [42]
```

Read the trace from the top: your line, then `Chanter::end()` running the cast, then the `Chanter::end()` line in your runite. A step inside PHP itself (a closure called by `array_map`, for example) has no file and shows as `[internal] [-]`.

## `glitch.txt`

Every glitch is also written to `.echoes/<runite>/glitch.txt`:

```
[2026-10-23 12:52:40] [EXCEPTION] [33] [/home/you/app/cast] The seal is broken.
```

`[time] [severity] [line] [file] message`.

`Keeper::begin()` empties the file at the start of every run, so it holds the glitch of the **last** run only. `keeper_is_glitch()` returns `true` when it is not empty.

## What a glitch does to the flow

1. The handler writes `glitch.txt`.
2. It clears the screen and shows the glitch screen.
3. It prints the footer and **exits**.

So `Keeper::end()` never runs: the [arcane](arcane.md) of a broken run is **not** written. `arcane.txt` still shows the run before.

## Reading a glitch

1. **Message** — what broke.
2. **Line and file** — where it broke.
3. **Trace** — which cast, which rune.
4. Still unsure? Run the cast again after one that works, then `grimoire --arcane` to see how far a good run goes.

## What you keep from this page

- `Keeper::begin()` catches every error, warning and exception.
- One glitch stops the flow; `glitch.txt` keeps the last one.
- The arcane of a broken run is not written.
- Next: [Beyond the Manifest](beyond-the-manifest.md)
