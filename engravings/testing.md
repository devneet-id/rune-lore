# Test Your Runite

> Give a runite its own `test` cast.

**Runes:** Whisper, Chanter · **From:** Act 0

```php
// php cast test
Chanter::cast('test', function() {
  $pass = 0; $fail = 0;
  $check = function(String $label, $ok) use (&$pass, &$fail) {
    $ok ? $pass++ : $fail++;
    Whisper::echo(($ok ? '{{color-success}} ✓ ' : '{{color-danger}} ✗ ') . $label . '{{nl}}');
  };

  // catch what a cast prints, and what it returns
  $out = Whisper::drain(fn() => Chanter::cast('greet --name=Rune')(), true);
  $check('greet prints the name', str_contains($out, 'Rune'));
  $check('double returns 8', Chanter::cast('double --n=4')() === 8);

  Whisper::echo(($fail ? '{{color-danger}}FAILED' : '{{color-success}}PASSED') . " $pass/" . ($pass + $fail) . '{{nl}}');
}, 'Test this runite.');

Chanter::cast('greet --name', fn() => Whisper::echo('Hello, ' . Chanter::spell('name') . '{{nl}}'));
Chanter::cast('double --n', fn() => 2 * (int) Chanter::spell('n'));
```

## How it works
- `Whisper::drain(fn, true)` catches what a cast prints, so you can check it.
- `Chanter::cast('x --a=1')()` returns what the cast returns.
- Pass spaces in spell values as `%20` when casting from code.
