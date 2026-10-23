# Cipher

> Cipher keeps the secrets of the system — and gives every thing a name of its own.

<!-- status: draft · sources: runes/cipher.md, scenario/02-notes, scenario/04-vault -->

→ Reference: [Cipher](../../runes/cipher.md)

## Numbers shift, ids don't
Remove `#1` and the old `#2` becomes `#1`. A cast that said `--edit=2` a moment ago now edits the wrong note. Give each note an id that never moves:

```php
$id = Cipher::id('n');      // n6adb5931aae18
$NOTES[$id] = $text;
```

`Cipher::id('n')` is a unique id with your prefix. The notes become `{ id: text }`, and edit and remove use the id:

```php
if (!isset($NOTES[$id])) return Whisper::echo("{{color-danger}}{{icon-danger}} No note $id{{nl}}");
…
unset($NOTES[$id]);
```

```bash
php cast note --add="Buy milk"
php cast note --add="Call mom"
php cast notes
php cast note --remove=n6adb5931aae18
```
```
[√] Added n6adb5931aae18
[√] Added n6adb5931b474d
#n6adb5931aae18 Buy milk
#n6adb5931b474d Call mom
2 notes
[!] Removed n6adb5931aae18
```

`notes.json` now reads:

```json
{
  "n6adb5931b474d": "Call mom",
  "n6adb5931f0b7d": "Water plants",
  "n6adb5931f0e54": "Read a book"
}
```

The row template needs no change — `{{note-id}}` simply holds the id now.

## Secrets
Cipher has more than ids:

| Call | Gives |
|---|---|
| `cipher_hash($text)` | a fast hash (xxh3) — the same text, the same hash |
| `Cipher::base64($text)` / `Cipher::base64($b64, 1)` | base64 and back |
| `Cipher::runic($text, false, 'elder_futhark')` / `…, true, …)` | text into runes and back |

The runic cipher is a **lore seal, not encryption**: it swaps lower-case letters for runes, one for one. Seal base64, not raw text. It is what seals your app in the [Artefact](artefact.md). → Recipe: [secrets](../../engravings/secrets.md)

## The runite at the end of Part II
Four runes from Act 0, three from the Sentinel, and the app remembers:

```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

use Rune\Aether\Manifest as Aether;
use Rune\Whisper\Manifest as Whisper;
use Rune\Weaver\Manifest as Weaver;
use Rune\Chanter\Manifest as Chanter;
use Rune\Forger\Manifest as Forger;
use Rune\Cipher\Manifest as Cipher;
use Rune\Keeper\Manifest as Keeper;
#sentinel-manifest
Aether::ether()::essence()::entity();
Whisper::ether()::essence()::entity();
Weaver::ether()::essence()::entity();
Chanter::ether()::essence()::entity();
Forger::ether()::essence()::entity();
Cipher::ether()::essence()::entity();
Keeper::ether()::essence()::entity();
#sentinel-awaken

Aether::begin();
Chanter::begin();
Keeper::begin();

// the notes live in .echoes/<runite>/notes.json as { id: text }
$NOTES = (array) (Keeper::item('notes') ?: []);
function notes_keep() {
  global $NOTES;
  return Keeper::item('notes', (object) $NOTES);
}

Chanter::cast('note --add --edit --remove --text', function() {
  global $NOTES;

  // create
  if ($text = Chanter::spell('add')) {
    if ($text === '1') $text = Whisper::call('Note: ');
    $id = Cipher::id('n');
    $NOTES[$id] = $text;
    notes_keep();
    Whisper::echo("{{color-success}}{{icon-success}} Added $id{{nl}}");
    return $id;
  }

  // update
  if ($id = Chanter::spell('edit')) {
    if (!isset($NOTES[$id])) return Whisper::echo("{{color-danger}}{{icon-danger}} No note $id{{nl}}");
    $text = Chanter::spell('text');
    if (!$text || $text === '1') $text = Whisper::call('New text: ');
    $NOTES[$id] = $text;
    notes_keep();
    return Whisper::echo("{{color-success}}{{icon-success}} Edited $id{{nl}}");
  }

  // delete
  if ($id = Chanter::spell('remove')) {
    if (!isset($NOTES[$id])) return Whisper::echo("{{color-danger}}{{icon-danger}} No note $id{{nl}}");
    unset($NOTES[$id]);
    notes_keep();
    return Whisper::echo("{{color-warning}}{{icon-warning}} Removed $id{{nl}}");
  }

  Chanter::cast('notes')();
}, 'Add, edit or remove a note. --add="text" --edit=<id> --text="text" --remove=<id>');

// read
Chanter::cast('notes', function() {
  global $NOTES;
  if (!$NOTES) return Whisper::echo('{{color-secondary}}No notes yet.{{nl}}');
  $row = Weaver::item(__DIR__ . '/weaver/row.txt');
  foreach ($NOTES as $id => $text) {
    Whisper::echo(Weaver::bind($row, ['note-id' => $id, 'note-text' => $text]));
  }
  Whisper::echo('{{color-secondary}}' . count($NOTES) . ' notes{{nl}}');
}, 'List the notes.');

// export: one note per line in export/notes.txt
Chanter::cast('export', function() {
  global $NOTES;
  $file = __DIR__ . '/export/notes.txt';
  Forger::fix(Forger::trace($file));
  Forger::item($file, implode(PHP_EOL, $NOTES) . PHP_EOL);
  Whisper::echo('{{color-success}}{{icon-success}} Exported ' . count($NOTES) . ' notes to export/notes.txt{{nl}}');
}, 'Write the notes to export/notes.txt.');

// import: every line of a text file becomes a note
Chanter::cast('import --file', function() {
  $file = Chanter::spell('file');
  if (!$file || $file === '1') $file = __DIR__ . '/export/notes.txt';
  if (!file_exists($file)) return Whisper::echo("{{color-danger}}{{icon-danger}} No file $file{{nl}}");
  $lines = array_filter(array_map('trim', explode("\n", Forger::item($file))));
  foreach ($lines as $line) {
    Chanter::cast('note --add=' . rawurlencode($line))();
  }
}, 'Add every line of a text file as a note. --file=notes.txt');

#sentinel-codex
Chanter::end();
Keeper::end();
Aether::end();
```

Next: [Artefact](artefact.md).
