# Manage Files

> A tiny file manager: create, read, back up and restore files in a folder.

**Runes:** Forger · **From:** Act 1

```php
// php cast box --new=hello.txt --text="Hello" | --read=hello.txt | --backup | --restore
define('BOX', AETHER_REPO . '/box');

Chanter::cast('box --new --text --read --backup --restore', function() {
  if ($name = Chanter::spell('new')) {
    Forger::fix(Forger::trace(BOX . "/$name"));
    Forger::item(BOX . "/$name", (string) Chanter::spell('text'));
  }
  if ($name = Chanter::spell('read')) {
    Whisper::echo(Forger::item(BOX . "/$name") . '{{nl}}');
  }
  if (Chanter::spell('backup')) {
    Forger::clone(BOX, BOX . '-backup');
  }
  if (Chanter::spell('restore')) {
    Forger::clean(BOX, true);
    Forger::move([['type' => 'repo', 'from' => BOX . '-backup', 'target' => BOX]]);
  }
  foreach (Forger::scan(BOX) as $item) {
    Whisper::echo('- ' . $item['basename'] . '{{nl}}');
  }
}, 'A tiny file manager in box/.');
```

## How it works
- `Forger::fix(Forger::trace($path))` creates every missing folder and the file itself.
- `Forger::item($path, $text)` writes, `Forger::item($path)` reads.
- `Forger::move()` **copies** (`item` = file, `repo` = folder). To move, `Forger::clean()` the source after.
- `Forger::clean($path, true)` removes a folder with everything inside.
