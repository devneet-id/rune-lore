# Cast and Spell

> A runite is a CLI app. You speak to it with casts and spells.

A **cast** is a command spoken to the runite. A **spell** is a word that shapes it. Before you engrave your own, learn to speak to one.

## The main hall
Run the runite with no cast:

```bash
php cast
```

```
 #  S T A T S.
 ♦ Main   » cast - 829.00B
 ♦ Repo   » /home/you/notes
 ♦ Rune   » Manifest=4, Ether=5, Essence=6, Entity=6
 ♦ Echoes »

 #  D E F A U L T.
 ♦ php8 cast grimoire
    ≈ Read the runes and the arcane of this
      runite.
 ♦ php8 cast reliquary
    ≈ Make, open and share relics (runite ⇄
      .rune).
 ♦ php8 cast sentinel
    ≈ Help you maintain your runite as an
      assistant.

 #  R E G I S T E R E D.
 ♦ php8 cast greet --name --loud
    ≈ Greet someone. --name=Anwar --loud

◇Version=1.20.114: ϟExecute=0.0038s, ΞMemory=926.56KB - ^1.10MB
```

- **DEFAULT** — the built-in runites every runite has: [grimoire](../../runites/grimoire.md), [reliquary](../../runites/reliquary.md), [sentinel](../../runites/sentinel.md). The main hall itself is the hidden cast [rune](../../runites/rune.md).
- **REGISTERED** — the casts *you* engrave.
- The `≈` line is the cast's **echo**: what it says of itself.

## A cast
```bash
php cast greet
```
```
[√] Hello, traveller
```

## A spell
A spell is an option after the cast: `--name` with a value, or `--loud` alone.

```bash
php cast greet --name=Anwar --loud
```
```
[√] HELLO, ANWAR
```

Inside the cast, `Chanter::spell('name')` reads it:

| You type | `Chanter::spell('name')` |
|---|---|
| `--name=Anwar` | `'Anwar'` |
| `--name` | `'1'` (given, no value) |
| *(nothing)* | `false` |
| `--name=0` | `'0'` |

## Spaces
On the command line, use quotes: `--name="Rune Lore"`. When you cast from code (you will in [Chanter](chanter.md)), write the space as `%20`: `'greet --name=Rune%20Lore'`.

## Zero trust
Add `--zero-trust` to any cast to run it with the arcane off and its output drained, then shown at once.

```bash
php cast greet --zero-trust
```

## The greet cast
This is the cast above. It is the first thing you will engrave in [Chanter](chanter.md).

```php
Chanter::cast('greet --name --loud', function() {
  $name = Chanter::spell('name');
  if (!$name || $name === '1') $name = 'traveller';
  $text = "Hello, $name";
  if (Chanter::spell('loud')) $text = strtoupper($text);
  Whisper::echo("{{color-success}}{{icon-success}} $text{{nl}}");
}, 'Greet someone. --name=Anwar --loud');
```

Next: [The App](the-app.md).
