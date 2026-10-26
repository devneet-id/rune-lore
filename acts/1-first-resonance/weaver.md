# Weaver

> Weaver turns raw data into text. Keep the shape of the output in a template; let Weaver fill it.

<!-- status: draft -->

→ Reference: [Weaver](../../runes/weaver.md)

## A template for one row
Make `weaver/row.txt` next to the runite:

```
{{color-info}}#{{note-id}}{{color-end}} {{note-text}}{{nl}}
```

`{{note-id}}` and `{{note-text}}` are yours. The other tokens are Whisper's — they stay until the echo.

## Load and bind
```php
Chanter::cast('notes', function() {
  global $NOTES;
  if (!$NOTES) return Whisper::echo('{{color-secondary}}No notes yet.{{nl}}');
  $row = Weaver::item(__DIR__ . '/weaver/row.txt');
  foreach ($NOTES as $i => $text) {
    Whisper::echo(Weaver::bind($row, ['note-id' => $i + 1, 'note-text' => $text]));
  }
}, 'List the notes.');
```

- `Weaver::item($file)` reads the template **once** and keeps it; the next call returns it from memory.
- `Weaver::bind($template, [...])` fills every token. `{{note-id}}` and `{{NOTE-ID}}` both match.

```
#1 Buy oat milk
#2 Call mom
```

Change the look of the list by editing `row.txt` — no code.

## The bond
Weaver remembers every value it binds. Read the last one back:

```php
Weaver::bond('note-text', null);   // 'Call mom'
```

Because the bond is shared, give your tokens specific names (`note-text`, not `text`) and avoid Whisper's own names (`nl`, `tab`, `end`, `bold`, `php`).

## Trap
Known issue: `weaver_item($file, [...])` with data glitches. Load with `Weaver::item()`, then fill with `Weaver::bind()` — as above.

Next: [Aether](aether.md).
