# Chanter

> Chanter is the gate of the command line. Every cast of the app passes through it.

<!-- status: draft · sources: runes/chanter.md, scenario/01-greeting, scenario/02-notes -->

You met casts as a user. Now engrave them. → Reference: [Chanter](../../runes/chanter.md)

## Register a cast
`Chanter::cast($cast, $fn, $echo)`:

- `$cast` — the name, then every spell it reads: `'note --add --edit --remove --text'`.
- `$fn` — what it does.
- `$echo` — the `≈` line on the main screen.

Casts are only **registered** here. `Chanter::end()` runs the one you typed.

## The app's casts
Add the two casts between `Chanter::begin()` and `#sentinel-codex`:

```php
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

Chanter::cast('notes', function() {
  global $NOTES;
  if (!$NOTES) return Whisper::echo('{{color-secondary}}No notes yet.{{nl}}');
  foreach ($NOTES as $i => $text) {
    Whisper::echo("{{color-info}}#" . ($i + 1) . "{{color-end}} $text{{nl}}");
  }
}, 'List the notes.');
```

- One cast, many spells: `note` checks `add`, then `edit`, then `remove`.
- `--add` alone gives `'1'`, so the app asks with `Whisper::call()` instead.
- `$NOTES` is global, so `global $NOTES;` inside each cast.

```bash
php cast note --add="Buy milk"
```
```
[√] Added #1
```

## Cast from code
A cast can call another cast. `Chanter::cast('name')` returns it; `()` runs it and gives back its return value.

```php
Chanter::cast('notes')();                          // the list, from inside "note"
$count = Chanter::cast('note --add=Buy%20milk')(); // 1 — spaces as %20
```

That is how `php cast note` (no spell) shows the list.

## Many casts in one run
Each `php cast …` is one run. To work with the notes in a single run, add a **session** — a cast that keeps asking for casts:

```php
Chanter::cast('session', function() {
  Whisper::echo('{{color-primary}}{{icon-primary}} Notes session. Type a cast (note --add=Milk, notes) or "exit".{{nl}}');
  while (($line = trim(Whisper::call('cast: '))) !== 'exit' && $line !== '') {
    Chanter::cast($line)();
  }
}, 'Work with the notes in one run.');
```

```
$ php cast session
[~] Notes session. Type a cast (note --add=Milk, notes) or "exit".
>>> cast: note --add=Buy%20milk
[√] Added #1
>>> cast: note --add=Call%20mom
[√] Added #2
>>> cast: note --edit=1 --text=Buy%20oat%20milk
[√] Edited #1
>>> cast: note --remove=2
[!] Removed #2
>>> cast: notes
#1 Buy oat milk
>>> cast: exit
```

The whole CRUD works — inside one run.

## Traps
- A spell set from code, `Chanter::spell('x', 'v')`, is read on the **next** cast. By design.
- Known issue: `chanter_cast_has()` always returns `false`. Don't rely on it yet.

Next: [Whisper](whisper.md).
