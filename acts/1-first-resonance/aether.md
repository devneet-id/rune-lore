# Aether

> Aether is the flow under the app. It opened the run, it will close it — and it can tell you what happened in between.

<!-- status: draft · sources: runes/aether.md -->

→ Reference: [Aether](../../runes/aether.md)

Aether's Manifest is small: `begin()`, `end()`, `dd()`, `exit()`. You met `begin` and `end` in [Act 0](../0-the-void/begin-and-end.md). Here are the other two, and a clock.

## Debug: `Aether::dd()`
Dump a value and stop the run:

```php
Chanter::cast('peek', function() {
  global $NOTES;
  Chanter::cast('note --add=Buy%20milk')();
  Aether::dd($NOTES);
}, 'Dump the notes with Aether::dd.');
```
```
[√] Added #1
///////////////////////////////////
 D I A G N O S T I C
 39  /root/rune/Aether/Manifest.php

array(1) » {
│ ♦ 0::string(8) » "Buy milk"
}
```

Nothing after `dd` runs — not even the footer. `Aether::exit()` stops the run too, but closes it properly: no dump, and the footer is printed.

## Time
How long has the flow been running? Aether keeps a stopwatch from `begin()`. Its Manifest has no method for it; call its Entity function directly (Act 2 goes deeper into this):

```php
Whisper::echo('{{color-secondary}}' . count($NOTES) . ' notes · ' . round(aether_stopwatch(), 4) . 's{{nl}}');
```
```
#1 Buy oat milk
1 notes · 0.0039s
```

`aether_memoryusage()` gives `[current, peak]` memory in bytes the same way.

## The footer, read again
Every run ends with Aether's footer:

```
◇Version=1.12.31: ϟExecute=0.0031s, ΞMemory=937.38KB - ^1.11MB
```

| Part | Meaning |
|---|---|
| `◇Version=` | the Rune version (`1.` + the sum of every rune's Phantasm version) |
| `ϟExecute=` | how long the run took |
| `ΞMemory=` | memory used, then `^` the peak |

Next: [It Forgets](it-forgets.md).
