# Many Runites

> Several apps in one folder, each with its own memory.

<!-- status: draft -->

One folder can hold many runites. Each is its own world — its own casts, its own `AETHER_FILE`, its own memory — while they share the folder's `vendor/` and `@liberations/`.

## One folder, two apps
```
my-app/
├── vendor/
├── @liberations/
│   └── Ledger/          shared by every runite in liberation mode
├── cast                 month, pack
├── wallet               add, book
└── .echoes/
    ├── cast/            memory of cast
    └── wallet/          memory of wallet (entries.json)
```
```bash
php cast              # the main screen of cast
php wallet            # the main screen of wallet — different casts
php wallet book
```
Nothing is mixed: `Keeper::item('entries')` in `wallet` never sees the items of `cast`.

## Runites that talk
A runite can cast another runite as a command and read its answer. Scenario `06-multicast` keeps three runites — `cast`, `ember`, `frost` — and relays a text through them:
```bash
php cast relay --text=hello     # cast → ember (upper) → frost (reverse)
```
The pattern (from [engravings/many-runites.md](../../engravings/many-runites.md)): run the other file with `PHP_BINARY`, read the line that starts with `=>`.
```php
function multicast( String $runite, Array $args ) {
  $command = 'cd ' . escapeshellarg(__DIR__) . ' && ' . escapeshellarg(PHP_BINARY) . ' ' . escapeshellarg($runite);
  foreach ($args as $arg) $command .= ' ' . escapeshellarg($arg);
  $out = preg_replace('/\x1b\[[0-9;]*[A-Za-z]/', '', (string) shell_exec($command . ' 2>&1'));
  return preg_match('/=> (.*)/', $out, $m) ? trim($m[1]) : false;
}
```
Inside **one** runite you do not need this — `Chanter::cast('x --a=1')()` returns the value ([Cast in Cast](../2-understanding-its-flow/cast-in-cast.md)). To run a runite beside the flow instead of waiting for it, use [Specter](specter.md): `Specter::cast('php ember count', ['visible' => false])`.

## When to split
- Two audiences (a user app and an admin tool) → two runites.
- Two memories that must never mix → two runites.
- Shared logic → not a runite: a [rune](engrave-a-rune.md) both runites invoke.
