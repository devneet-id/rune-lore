# Runes Lean on Runes

> No rune stands alone.

Each rune has one purpose. To do it, it borrows the hands of others: Keeper remembers by writing files with Forger, Crafter bundles with Weaver's templates, Aether speaks its footer through Whisper. The Phantasm writes these bonds down.

## The `link` of a Phantasm

Every Phantasm has a `link` list: `[rune, what it uses, version]`.

```php
// Keeper/Phantasm.php
public $link = [
  ['Aether', 'ether', '1.17'],
  ['Chanter', 'entity', '1.13'],
  ['Cipher', 'entity', '1.6'],
  ['Forger', 'entity', '1.14'],
  ['Specter', 'entity', '1.9'],
  ['Whisper', 'entity', '1.13'],
];
```

Read it live:

```
$ php cast grimoire --rune=Keeper
  ::L I N K
    Aether ether 1.17
    Chanter entity 1.13
    Cipher entity 1.6
    Forger entity 1.14
    Specter entity 1.9
    Whisper entity 1.13
```

## Who leans on whom

| Rune | Leans on |
|---|---|
| Aether | Chanter, Whisper |
| Whisper | Aether, Weaver |
| Weaver | Aether |
| Chanter | Aether, Whisper, Specter |
| Forger | Aether, Keeper |
| Cipher | Aether |
| Keeper | Aether, Chanter, Cipher, Forger, Specter, Whisper |
| Crafter | Aether, Cipher, Forger, Weaver, Whisper |

Specter appears in some links; you meet it in [Act 3](../3-liberation-of-forte/README.md). Those links are soft — read on.

## Hard and soft bonds

Not every link is a must.

- **Soft:** the rune asks first. Aether prints a plain footer when Whisper is not awake; Chanter and Keeper only call Specter when it is there.

  ```php
  // Aether/Entity.php — aether_exit()
  if (aether_has_entity('whisper')) {
    // the coloured footer
  } else {
    print("\n\nRUNE: Execute=...");
  }
  ```

- **Hard:** the rune just calls. Keeper calls `forger_fix()` in `begin()`; Crafter calls `forger_item()`, `weaver_bind()` and `cipher_id()` while it bundles. Without them the flow dies (see [The Flow](the-flow.md#why-the-order-matters)).

When unsure, awaken every rune the link names — or read it in the [Grimoire](../../runites/grimoire.md).

## What is awake right now

| Ask | Answer |
|---|---|
| `aether_has_entity('forger')` | `true` when the Forger Entity is loaded (it checks `function_exists`) |
| `aether_arised()` | the Manifest classes that were awakened |
| `aether_list_runes()` | the rune folders whose Phantasm counts in the footer — awake or not |

```php
Chanter::cast('awake', function() {
  foreach (aether_arised() as $rune) {
    Whisper::echo("{{icon-success}} $rune{{nl}}");
  }
  Whisper::echo('Forger awake: ' . (aether_has_entity('forger') ? 'yes' : 'no') . '{{nl}}');
}, 'Which runes are awake.');
```

```
$ php cast awake
[√] Rune\Whisper\Manifest
[√] Rune\Weaver\Manifest
[√] Rune\Chanter\Manifest
[√] Rune\Forger\Manifest
[√] Rune\Cipher\Manifest
[√] Rune\Keeper\Manifest
[√] Rune\Aether\Manifest
Forger awake: yes
```

## What you keep from this page

- The Phantasm `link` tells you what a rune needs.
- Soft bonds ask with `aether_has_entity()`; hard bonds just call.
- Next: [Arcane](arcane.md)
