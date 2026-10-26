# Many Runites in One Folder

> Split an app into several runites that call each other.

**Runes:** Chanter, Keeper · **From:** Act 3

```php
// cast (the hub) calls another runite in the same folder: php ember upper --text=hi
function multicast( String $runite, Array $args ) {
  $command = 'cd ' . escapeshellarg(__DIR__) . ' && ' . escapeshellarg(PHP_BINARY) . ' ' . escapeshellarg($runite);
  foreach ($args as $arg) $command .= ' ' . escapeshellarg($arg);
  $out = preg_replace('/\x1b\[[0-9;]*[A-Za-z]/', '', (string) shell_exec($command . ' 2>&1'));
  return preg_match('/=> (.*)/', $out, $m) ? trim($m[1]) : false;   // the other runite answers with "=> ..."
}

Chanter::cast('relay --text', function() {
  $fire = multicast('ember', ['upper', '--text=' . Chanter::spell('text')]);
  $ice  = multicast('frost', ['reverse', "--text=$fire"]);
  Whisper::echo("=> $ice{{nl}}");
}, 'Pass a text through ember, then frost.');

// inside one runite: a cast returns a value to the cast that called it
Chanter::cast('double --n', fn() => 2 * (int) Chanter::spell('n'));
Chanter::cast('chain --n', function() {
  $doubled = Chanter::cast('double --n=' . Chanter::spell('n'))();
  Whisper::echo("=> $doubled{{nl}}");
});
```

## How it works
- Each runite is its own world: its own casts, `AETHER_FILE`, and memory in `.echoes/<runite>/`.
- Across runites, call the other file with PHP and read its answer (a line starting with `=>`).
- Inside one runite, `Chanter::cast('x --a=1')()` runs a cast and returns its value.
