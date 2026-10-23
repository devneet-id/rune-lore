# Cipher

> Keeps secrets and identities of the system—unique ids, fast hashes, base64 and runic cipher that turns text into runes and back, used to seal artefacts.

Cipher keeps the secrets of the system: unique ids, fast hashes, base64, and the **runic cipher** that turns text into runes and back. Artefacts are sealed with it.

| | |
|---|---|
| **Version** | `1.6` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 1 · First Resonance |
| **Uses** | [Aether](aether.md) (entity) |
| **Awaken** | `use Rune\Cipher\Manifest as Cipher;` · `Cipher::ether()::essence()::entity();` |

## When to use
- Id: `Cipher::id('prefix')`.
- Hash: `cipher_hash($text)` (xxh3).
- Seal: `Cipher::runic(Cipher::base64($text), false, 'elder_futhark')`; open with the same variant and `true`.

## In code
```php
Chanter::cast('seal --text', function() {
  $text = Chanter::spell('text') ?: 'hello rune';

  Whisper::echo('id      ' . Cipher::id('n') . '{{nl}}');
  Whisper::echo('hash    ' . cipher_hash($text) . '{{nl}}');

  $base64 = Cipher::base64($text);
  $runic  = Cipher::runic($base64, false, 'elder_futhark');
  Whisper::echo('runic   ' . $runic . '{{nl}}');

  $back = Cipher::base64(Cipher::runic($runic, true, 'elder_futhark'), 1);
  Whisper::echo('back    ' . $back . '{{nl}}');
}, 'Seal a text with the runic cipher. --text="..."');
```

## Manifest
Call from your runite: `Cipher::name(...)`.

| Method | Note |
|---|---|
| `_arise()` | *Legacy hook — not called by Aether.* |
| `id( String $prefix = "", $entropy = false )` | Generates unique cipher ID with optional prefix and entropy. |
| `base64( String $text, Int $isDecode = 0 )` | Encodes or decodes Base64 text based on the given flag. |
| `runic( String $text, Bool $isDecode = false, String $variant = "default" )` | Encodes or decodes text using runic character mapping. |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `cipher()` | Placeholder function that currently returns true, possibly for future cipher logic. |
| `cipher_id( String $prefix = "", $entropy = false )` | Generates a unique ID using optional prefix and entropy (via uniqid). |
| `cipher_hash( String $text )` | Creates a fast and lightweight hash of the input text using "xxh3" algorithm. |
| `cipher_base64( String $text, Int $isDecode = 0 )` | Encodes or decodes Base64 based on $isDecode flag (0 = encode, 1 = decode). |
| `cipher_runic( String $text, Bool $isDecode = false, String $variant = "default" )` | Main handler for encoding or decoding runic cipher text using helper functions based on $isDecode flag. |
| `cipher_runic_encode( String $text, String $variant = "default" )` | Encodes plain text into runic characters based on the selected variant mapping from CIPHER_RUNIC. |
| `cipher_runic_decode( String $text, String $variant = "default")` | Decodes runic characters back into plain text by flipping the selected variant mapping from CIPHER_RUNIC. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `CIPHER` | Acts as a flag to indicate that the CIPHER system is enabled. |
| `CIPHER_RUNIC_LIST` | Contains a list of supported runic cipher variants for encoding/decoding |
| `CIPHER_RUNIC` | Holds the character mapping tables for each runic cipher variant (e.g., default, elder futhark, etc). |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$CIPHER` | main essence |

## Notes
- Variants: `default`, `elder_futhark`, `younger_futhark`, `anglo_saxon_futhorc` (`CIPHER_RUNIC_LIST`). Every variant maps one letter to one rune.
- Only lower-case letters are changed; numbers, upper case and symbols stay — so seal base64, not raw text.
- The runic cipher is a lore seal, not encryption.

---
*Generated from `Cipher/Phantasm.php` (version 1.6). Read it live with `php cast grimoire --rune=Cipher`.*
