# Your First Runite

> Cast it once and read what comes back.

The void answers when you speak to it. Run the runite you just awakened, then teach it one word of your own.

## The main screen
```bash
php cast
```
```
 #  S T A T S.
 ♦ Main   » cast - 1.18KB
 ♦ Repo   » /home/you/my-runite
 ♦ Rune   » Manifest=4, Ether=5, Essence=6, Entity=6
 ♦ Echoes »

 #  D E F A U L T.
 ♦ php cast artefact
    ≈ To handle with shard & artefact.
 ♦ php cast grimoire
    ≈ will help you read the system structure
      and flow.
 ♦ php cast rune
    ≈ base of the rune
 ♦ php cast sentinel
    ≈ Help you with maintain your runite as
      assistant.

 #  R E G I S T E R E D.

◇Version=1.12.31: ϟExecute=0.0039s, ΞMemory=923.52KB - ^1.10MB
```
*(The banner above STATS is left out here.)*

- **STATS** — your runite, the folder, how many rune parts are awake. **Echoes** is empty: nothing is kept yet.
- **DEFAULT** — the built-in casts that `Chanter::begin()` loaded.
- **REGISTERED** — your own casts. Empty, for now.

More: [the main screen](../../runites/rune.md).

## One cast, one spell
Replace `// ✦ Main logic lives here` with:

```php
Chanter::cast('greet --name', function() {
  $name = Chanter::spell('name');
  if (!$name || $name === '1') {
    $name = 'traveller';
  }
  $line = Weaver::bind('Welcome, {{who}}. The void is quiet.', ['who' => $name]);
  Whisper::echo("{{color-success}}{{icon-success}}{{color-end}} $line{{nl}}");
}, 'Greet someone from the void.');
```

Every rune of this Act is here:

| Line | Rune | What it does |
|---|---|---|
| `Chanter::cast('greet --name', fn, 'Greet …')` | Chanter | registers the cast `greet`, its spell `--name`, and its echo (the note) |
| `Chanter::spell('name')` | Chanter | reads `--name`: `false` when missing, `'1'` when given without a value |
| `Weaver::bind($text, [...])` | Weaver | fills `{{who}}` with the name |
| `Whisper::echo(...)` | Whisper | prints, with a color and an icon |
| begin, end, footer | Aether | carries the whole flow |

## Cast it
```bash
php cast greet
php cast greet --name=Anwar
php cast greet --name="Anwar Achilles"
```
```
[√] Welcome, traveller. The void is quiet.
[√] Welcome, Anwar. The void is quiet.
[√] Welcome, Anwar Achilles. The void is quiet.
```
Each run ends with the footer. Run `php cast` again: your cast now stands under **REGISTERED**, with its echo.

```
 #  R E G I S T E R E D.
 ♦ php cast greet --name
    ≈ Greet someone from the void.
```

## Read the footer
```
◇Version=1.12.31: ϟExecute=0.0051s, ΞMemory=921.83KB - ^1.10MB
```
The Rune version, how long it took, and how much memory it used. See [Begin and End](begin-and-end.md#the-footer).

## No echoes yet
Look at your folder: still only `cast` and `vendor/`. Run `greet` a hundred times and nothing is kept. The runite flows, speaks and forgets. That changes in [Act 1 · First Resonance](../1-first-resonance/README.md), where Keeper brings `.echoes`.

Next: [Reading the Grimoire](reading-the-grimoire.md)
