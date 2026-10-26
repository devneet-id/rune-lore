# It Forgets

> The app works. Run it twice and the notes of the first run are gone.

The four runes live inside one flow. When `Aether::end()` closes the flow, everything the flow held is gone.

## See it
```bash
php cast note --add="Buy milk"
php cast note --add="Buy milk"
php cast notes
```
```
[√] Added #1
[√] Added #1
No notes yet.
```

Both adds say `#1`. Each run starts with `$NOTES = []`, adds one note, and ends. The third run starts empty again.

The [session](chanter.md#many-casts-in-one-run) hid this: inside one run, the CRUD works. Leave the session and the notes go with it.

## Nothing is kept
Look at the folder:

```
notes/
├── cast
├── vendor/
└── weaver/
```

No `.echoes`. Aether, Whisper, Weaver and Chanter only *know* where `.echoes` would be — none of them writes it. The Grimoire says the same:

```bash
php cast grimoire --arcane
```
```
[!] No arcane recorded yet.
 Engrave Keeper in your runite (Keeper::begin() ... Keeper::end()) to record the arcane.
```

## The runite at the end of Part I
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

Chanter::cast('note --add --edit --remove --text', function() {
  global $NOTES;

  // create
  if ($text = Chanter::spell('add')) {
    if ($text === '1') $text = Whisper::call('Note: ');
    $NOTES[] = $text;
    Whisper::echo('{{color-success}}{{icon-success}} Added #' . count($NOTES) . '{{nl}}');
    return count($NOTES);
  }

  // update
  if ($id = Chanter::spell('edit')) {
    if (!isset($NOTES[$id - 1])) return Whisper::echo("{{color-danger}}{{icon-danger}} No note #$id{{nl}}");
    $text = Chanter::spell('text');
    if (!$text || $text === '1') $text = Whisper::call('New text: ');
    $NOTES[$id - 1] = $text;
    return Whisper::echo("{{color-success}}{{icon-success}} Edited #$id{{nl}}");
  }

  // delete
  if ($id = Chanter::spell('remove')) {
    if (!isset($NOTES[$id - 1])) return Whisper::echo("{{color-danger}}{{icon-danger}} No note #$id{{nl}}");
    array_splice($NOTES, $id - 1, 1);
    return Whisper::echo("{{color-warning}}{{icon-warning}} Removed #$id{{nl}}");
  }

  Chanter::cast('notes')();
}, 'Add, edit or remove a note. --add="text" --edit=1 --text="text" --remove=1');

// read
Chanter::cast('notes', function() {
  global $NOTES;
  if (!$NOTES) return Whisper::echo('{{color-secondary}}No notes yet.{{nl}}');
  $row = Weaver::item(__DIR__ . '/weaver/row.txt');
  foreach ($NOTES as $i => $text) {
    Whisper::echo(Weaver::bind($row, ['note-id' => $i + 1, 'note-text' => $text]));
  }
  Whisper::echo('{{color-secondary}}' . count($NOTES) . ' notes · ' . round(aether_stopwatch(), 4) . 's{{nl}}');
}, 'List the notes.');

// debug: dump the notes and stop
Chanter::cast('peek', function() {
  global $NOTES;
  Chanter::cast('note --add=Buy%20milk')();
  Aether::dd($NOTES);
}, 'Dump the notes with Aether::dd.');

// a session: many casts in one run
Chanter::cast('session', function() {
  Whisper::echo('{{color-primary}}{{icon-primary}} Notes session. Type a cast (note --add=Milk, notes) or "exit".{{nl}}');
  while (($line = trim(Whisper::call('cast: '))) !== 'exit' && $line !== '') {
    Chanter::cast($line)();
  }
}, 'Work with the notes in one run.');

#sentinel-codex
Chanter::end();
Aether::end();
```

## Three more runes
To remember, the app needs **Keeper**. To write files, **Forger**. To give each note an id that never shifts, **Cipher**. You don't type them in by hand — the [Sentinel](sentinel.md) brings them.
