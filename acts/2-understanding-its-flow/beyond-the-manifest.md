# Beyond the Manifest

> The Manifest is the face; the rune is deeper.

<!-- status: draft -->

Until now you called runes by their face: `Forger::item()`, `Whisper::echo()`. Behind every face are three more layers you awakened yourself — **Ether**, **Essence** and **Entity**. They are open to your runite too.

## Three layers, three kinds of PHP

| Layer | PHP | Named | Example |
|---|---|---|---|
| **Ether** | constants (`define`) | `RUNE_NAME` | `AETHER_FILE`, `AETHER_REPO`, `KEEPER_ECHOES` |
| **Essence** | globals | `$RUNE_NAME` | `$CHANTER_ECHO`, `$AETHER_ARCANE`, `$KEEPER_ARCANE` |
| **Entity** | functions | `rune_name()` | `cipher_hash()`, `forger_trace()`, `aether_formatFileSize()` |

The Manifest itself is thin: most of its methods call one Entity function and write an arcane line. `Forger::fix()` is `forger_fix()` plus a trace.

## In code

```php
Chanter::cast('inside', function() {
  global $CHANTER_ECHO;

  // Ether — constants
  Whisper::echo('runite : ' . AETHER_FILE . '{{nl}}');
  Whisper::echo('echoes : ' . basename(KEEPER_ECHOES) . '{{nl}}');

  // Entity — functions
  Whisper::echo('hash   : ' . cipher_hash('rune') . '{{nl}}');
  Whisper::echo('size   : ' . aether_formatFileSize(filesize(AETHER_FILE)) . '{{nl}}');

  // Essence — globals (read only)
  Whisper::echo('casts  : ' . implode(', ', array_keys($CHANTER_ECHO)) . '{{nl}}');
}, 'Look inside the runes.');
```

```
$ php cast inside
runite : cast
echoes : cast
hash   : 81816020bfa33c0a
size   : 2.77KB
casts  : artefact, grimoire, rune, sentinel, hello, break, warn, ...
```

## When to go deeper

| Use | When |
|---|---|
| **Manifest** | almost always — it is the stable face, and it leaves a trace in the [arcane](arcane.md) |
| **Entity** | a helper the Manifest does not show (`cipher_hash`, `aether_formatFileSize`, `weaver_wrap_word`), or an option it hides (`weaver_bind_multiple($t, $data, false)` binds without saving to the bond) |
| **Ether** | to know *where*: the runite's name, its folder, its echoes |
| **Essence** | to *read* the state of the flow: the casts, the arcane, the spells |

## Read Essence, don't write it

Essence is the living state of the flow. Change it by hand and a rune may stop making sense:

- Read `$CHANTER_ECHO` to list casts — fine.
- Write `$CHANTER_SPELL` — use `Chanter::spell('x', 'v')` instead.
- Empty `$AETHER_ARCANE` — use `aether_arcane_reset()` if you must.

Inside a function, reach an Essence with `global $NAME;` or `$GLOBALS['NAME']`.

## Where to find them

Every node is in the Phantasm. Read one rune at a time:

```
$ php cast grimoire --rune=Cipher
```

Or open the reference: [runes/](../../runes/README.md) lists every Manifest method, Entity function, Ether constant and Essence global, rune by rune.

## What you keep from this page

- Ether = constants, Essence = globals, Entity = functions — all open to you.
- Prefer the Manifest; go deeper for helpers and for knowing *where*.
- Read Essence; change it only through the rune.
- Next: [Cast in Cast](cast-in-cast.md)
