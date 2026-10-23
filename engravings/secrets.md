# Seal a Secret

> Keep a value sealed with the runic cipher.

**Runes:** Cipher, Keeper · **From:** Act 1

```php
// php cast secret --set=wifi --value=hunter2 | --get=wifi
Chanter::cast('secret --set --value --get', function() {
  $vault = Keeper::item('vault') ?: new stdClass;
  $variant = 'elder_futhark';

  if ($key = Chanter::spell('set')) {
    $vault->$key = Cipher::runic(Cipher::base64((string) Chanter::spell('value')), false, $variant);
    Keeper::item('vault', $vault);
    Whisper::echo("Sealed $key{{nl}}");
  }
  if (($key = Chanter::spell('get')) && isset($vault->$key)) {
    Whisper::echo("$key = " . Cipher::base64(Cipher::runic($vault->$key, true, $variant), 1) . '{{nl}}');
  }
}, 'Seal and open a secret.');
```

## How it works
- Seal = base64, then runic. Open = runic back, then base64 decode. Use the same variant both ways.
- Variants: `default`, `elder_futhark`, `younger_futhark`, `anglo_saxon_futhorc`.
- The runic cipher is a lore seal, not encryption — don't keep real passwords this way.

**Full, tested example:** `rune-dev/scenario/04-vault`
