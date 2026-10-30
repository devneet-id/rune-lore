# Minister

> Speaks with a familiar (an AI spirit) on behalf of the runite—asks questions, gathers the answers, and brings them back into the flow.

Minister speaks with a **familiar** — an AI spirit — on behalf of the runite, and brings its answers back into the flow.

| | |
|---|---|
| **Version** | `0.3` |
| **Mark** | `DEVELOPMENT` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 3 · Liberation of Forte |
| **Uses** | [Aether](aether.md) (entity), [Keeper](keeper.md) (ether:entity), [Whisper](whisper.md) (entity) |
| **Awaken** | `use Rune\Minister\Manifest as Minister;` · `Minister::ether()::essence()::entity();` |

## When to use
- Ask: `Minister::ask('question')` returns the answer or `false`.
- Collect: `Minister::say()` returns every answer of this run.

## In code
```php
// .echoes/<runite>/familiar.json → {"url": "https://...", "token": "...", "model": "gemini"}
Chanter::cast('ask --question', function() {
  $answer = Minister::ask(Chanter::spell('question') ?: 'What is a rune?');
  if ($answer !== false) {
    Whisper::echo($answer . '{{nl}}');
  }
}, 'Ask the familiar. --question="..."');
```

## Manifest
Call from your runite: `Minister::name(...)`.

| Method | Note |
|---|---|
| `ask( Array\|String $texts )` | Asks the familiar (AI spirit) and returns its answer |
| `say()` | Returns every answer collected from the familiar |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `minister()` | Main entity |
| `minister_familiar()` | Reads the familiar (spirit) kept by Keeper in .echoes/&lt;runite&gt;/familiar.json as {"url": "", "token": ""} |
| `minister_http( String $url, Array $headers, Array $body )` | Sends a JSON request to the familiar and returns the raw response body |
| `minister_ask( Array $texts )` | Asks the familiar (AI spirit) and keeps its answer |
| `minister_say()` | Returns every answer collected from the familiar |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `MINISTER` | Flag to indicate the Minister system is active. |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$MINISTER_RESPONSE` | Answers collected from the familiar. |

## Notes
- The familiar is `.echoes/<runite>/familiar.json`: `{"url": "...", "token": "...", "model": "gemini"}`. Keeper must be engraved.
- Without a familiar, Minister warns and returns `false`.
- Minister is still being shaped; its mark will follow the VOID pattern.

---
*Generated from `Minister/Phantasm.php` (version 0.3). Read it live with `php cast grimoire --rune=Minister`.*
