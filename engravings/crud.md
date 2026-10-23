# Keep Data (CRUD)

> Add, list, edit and delete records that survive between runs.

**Runes:** Chanter, Cipher, Keeper · **From:** Act 1

```php
// php cast note --add="Buy milk" | notes | note --edit=<id> --text="..." | note --delete=<id>
function notes_load() {
  $notes = Keeper::item('notes');
  return $notes ? json_decode(json_encode($notes), true) : [];
}

Chanter::cast('note --add --edit --text --delete', function() {
  $notes = notes_load();

  if ($text = Chanter::spell('add')) {
    $id = Cipher::id('n');
    $notes[$id] = ['id' => $id, 'text' => $text];
    Whisper::echo("Added $id{{nl}}");
  } elseif (($id = Chanter::spell('edit')) && isset($notes[$id])) {
    $notes[$id]['text'] = Chanter::spell('text');
    Whisper::echo("Updated $id{{nl}}");
  } elseif (($id = Chanter::spell('delete')) && isset($notes[$id])) {
    unset($notes[$id]);
    Whisper::echo("Deleted $id{{nl}}");
  }

  Keeper::item('notes', (object) $notes);   // (object): an empty list is still saved
}, 'Add, edit or delete a note.');

Chanter::cast('notes', function() {
  foreach (notes_load() as $note) {
    Whisper::echo("{{color-info}}{$note['id']}{{color-end}} {$note['text']}{{nl}}");
  }
}, 'List notes.');
```

## How it works
- `Keeper::item('notes')` reads `.echoes/<runite>/notes.json` (an object, or `null`). `json_decode(json_encode(...), true)` turns it into an array.
- Save with `(object)`: an empty array would be read as *get*, not *set*.
- `Cipher::id('n')` gives every record a unique id.
- Remember `Keeper::begin()` / `Keeper::end()` in the runite — see [Traps](traps.md).

**Full, tested example:** `rune-dev/scenario/02-notes` (and `05-todo`)
