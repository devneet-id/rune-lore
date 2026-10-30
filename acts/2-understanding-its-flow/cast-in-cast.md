# Cast in Cast

> A cast can call another cast.

A cast is not only for the command line. Inside your runite it is a callable you can fetch and run — so small casts become steps of bigger ones, and one runite becomes a chain of chants.

## Get a cast, then run it

`Chanter::cast('name')` without a callable **gets** the cast. Add `()` to run it. It gives back what the cast returns.

```php
Chanter::cast('hello --name', function() {
  $name = Chanter::spell('name') ?: 'traveler';
  Whisper::echo(Weaver::bind('Hello, {{name}}.{{nl}}', ['name' => $name]));
  return $name;
}, 'Say hello.');

Chanter::cast('greet-all', function() {
  $names = [];
  foreach (['Rune', 'Ember', 'Frost'] as $name) {
    $names[] = Chanter::cast("hello --name=$name")();
  }
  Whisper::echo('{{color-success}}{{icon-success}} Greeted ' . count($names) . ' names.{{nl}}');
}, 'Cast hello three times from code.');
```

```
$ php cast greet-all
Hello, Rune.
Hello, Ember.
Hello, Frost.
[√] Greeted 3 names.
```

A name that does not exist still gives a callable — one that warns and guesses:

```
$ php cast helo
[!]WARNING: Chanter cast with 'helo' not found.
[i]INFO: You mean: hello,
```

## Spells from code

From code, the cast string is split **by spaces**. A space inside a value cuts it.

```php
Chanter::cast('hello --name=Old%20Friend')();   // Hello, Old Friend.
Chanter::cast('hello --name=Old Friend')();     // cast 'hello Friend' not found
```

Use `%20` for spaces. On the command line, quotes work as usual: `php cast hello --name="Old Friend"`.

## Spells of the outer cast are replaced

Running an inner cast reads **its** spells. After it returns, the outer cast's spells are gone.

```php
Chanter::cast('outer --tag', function() {
  Whisper::echo('before: ' . var_export(Chanter::spell('tag'), true) . '{{nl}}');
  Chanter::cast('hello --name=Inner')();
  Whisper::echo('after:  ' . var_export(Chanter::spell('tag'), true) . '{{nl}}');
}, 'Spells of the outer cast after an inner cast.');
```

```
$ php cast outer --tag=blue
before: 'blue'
Hello, Inner.
after:  false
```

**Read every spell first**, keep them in variables, then cast.

## Setting a spell from code

`Chanter::spell('name', 'Echo')` does not change the spells you are reading now. It is read by the **next** cast — by design.

```php
Chanter::cast('later', function() {
  Chanter::spell('name', 'Echo');
  Whisper::echo('now:   ' . var_export(Chanter::spell('name'), true) . '{{nl}}');
  Chanter::cast('hello')();
}, 'Set a spell from code and see when it is read.');
```

```
$ php cast later
now:   false
Hello, Echo.
```

## Drain — run it quietly

`Whisper::drain(fn, true)` runs a callable and gives back what it would have printed, instead of printing it.

```php
Chanter::cast('quiet', function() {
  $text = Whisper::drain(function() {
    Chanter::cast('hello --name=Shadow')();
  }, true);
  Whisper::echo('Caught: ' . trim(preg_replace('/\e\[[0-9;]*m/', '', $text)) . '{{nl}}');
}, 'Catch what hello says instead of printing it.');
```

```
$ php cast quiet
Caught: Hello, Shadow.
```

The drained text still carries Whisper's colours; strip them as above when you need plain text.

## Zero trust

`--zero-trust` works on any cast:

```
$ php cast hello --name=Anwar --zero-trust
Hello, Anwar.

◇Version=1.20.110: ϟExecute=0.0040s, ΞMemory=1.10MB - ^1.28MB
```

What changes:

- The [arcane](arcane.md) is turned off — nothing is traced.
- The cast runs inside a drain; its output is printed at once when it ends.
- The flow exits right after the cast: `Keeper::end()` is **not** reached, so `arcane.txt` keeps the run before.
- The footer marks it: `ϟ` turns warning-coloured and `Ξ` danger-coloured.

## What you keep from this page

- `Chanter::cast('name --x=1')()` runs a cast and returns its value.
- `%20` for spaces; read outer spells before casting inner ones.
- `Whisper::drain()` catches output; `--zero-trust` runs without a trace.
- Next: [Resonance](resonance.md)
