# Forger

> Forger shapes files and folders. With it, the app can write its notes to a file — and read them back.

→ Reference: [Forger](../../runes/forger.md)

Keeper keeps the app's own memory inside `.echoes`. Forger works with files anywhere — files a person can open, send, or edit.

## Export
```php
Chanter::cast('export', function() {
  global $NOTES;
  $file = __DIR__ . '/export/notes.txt';
  Forger::fix(Forger::trace($file));
  Forger::item($file, implode(PHP_EOL, $NOTES) . PHP_EOL);
  Whisper::echo('{{color-success}}{{icon-success}} Exported ' . count($NOTES) . ' notes to export/notes.txt{{nl}}');
}, 'Write the notes to export/notes.txt.');
```

Three steps, always in this order:

1. `Forger::trace($file)` — walks the path and marks what exists and what is missing.
2. `Forger::fix(...)` — makes what is missing: the `export/` folder, the empty file.
3. `Forger::item($file, $text)` — writes. It writes **only** when the folder exists — that is why `fix` comes first.

```bash
php cast export
cat export/notes.txt
```
```
[√] Exported 2 notes to export/notes.txt
Buy oat milk
Call mom
```

## Import
`Forger::item($file)` with no text **reads**:

```php
Chanter::cast('import --file', function() {
  $file = Chanter::spell('file');
  if (!$file || $file === '1') $file = __DIR__ . '/export/notes.txt';
  if (!file_exists($file)) return Whisper::echo("{{color-danger}}{{icon-danger}} No file $file{{nl}}");
  $lines = array_filter(array_map('trim', explode("\n", Forger::item($file))));
  foreach ($lines as $line) {
    Chanter::cast('note --add=' . rawurlencode($line))();
  }
}, 'Add every line of a text file as a note. --file=notes.txt');
```

Each line becomes a note through the `note --add` cast — cast from code, with `rawurlencode()` turning spaces into `%20`.

```bash
printf 'Water plants\nRead a book\n' > todo.txt
php cast import --file=todo.txt
```
```
[√] Added #3
[√] Added #4
```

## More
`item` is a file, `repo` a folder. Forger also scans, moves (copies), clones and cleans — see the [reference](../../runes/forger.md) and the [files recipe](../../engravings/files.md).

Next: [Cipher](cipher.md).
