# Whisper

> Handles user-facing output through styled messages, prompts, and echoes—focused on delivering clear, customizable system feedback and visual communication.

Whisper is the voice of the runite. Everything the user reads passes through it: colors, icons, labels, questions, and silence (the drain).

| | |
|---|---|
| **Version** | `1.13` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles, Kuro Kid |
| **Introduced in** | Act 0 · The Void |
| **Uses** | [Aether](aether.md) (entity), [Weaver](weaver.md) (entity) |
| **Awaken** | `use Rune\Whisper\Manifest as Whisper;` · `Whisper::ether()::essence()::entity();` |

## When to use
- Print with `Whisper::echo('{{color-success}}{{icon-success}} Done{{nl}}')`.
- Ask with `Whisper::call('Your name: ')`.
- Catch output instead of printing it with `Whisper::drain(fn, true)`.

## In code
```php
Chanter::cast('speak', function() {
  Whisper::clear();
  Whisper::echo('{{color-success}}{{icon-success}} Saved{{nl}}');
  Whisper::echo('{{color-warning}}{{icon-warning}} Careful{{nl}}');
  Whisper::echo('{{label-info}}a labelled line{{nl}}');

  // drain: catch the output instead of printing it
  $caught = Whisper::drain(fn() => Whisper::echo('inside the drain'), true);
  Whisper::echo('caught: ' . strlen($caught) . ' bytes{{nl}}');

  // call: ask the user (needs a terminal)
  // $name = Whisper::call('Your name: ');
}, 'Speak with colors, icons and labels.');
```

## Manifest
Call from your runite: `Whisper::name(...)`.

| Method | Note |
|---|---|
| `_arise()` | *Legacy hook — not called by Aether.* |
| `_aether_end()` | *Legacy hook — not called by Aether.* |
| `end()` | Final phase of the class lifecycle, called after all manifest components are registered and ready. |
| `echo( String $message, Bool $asString = false )` | Print or return a formatted whisper message with color support |
| `call( String $text )` | Prompt user for input through STDIN with a whisper message |
| `drain( Mixed $state_or_process, Bool $asString = false )` | Start, process, or return a buffered whisper output (drain mode) |
| `clear( Bool $force = false )` | Clear terminal screen, optionally forcing it for cross-platform |
| `flash( Callable $execute )` | wrapper to control flash with callbacks |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `whisper()` | main entity |
| `whisper_clear()` | Clear terminal screen using ANSI escape codes |
| `whisper_clear_force()` | Force clear terminal using system commands (Linux & Windows) |
| `whisper_delay( Int $ms )` | Delay output for a given number of milliseconds |
| `whisper_echo( String $message, Bool $asString = false )` | Display or retrieve a formatted message with color/icon support |
| `whisper_echo_get( String $message )` | Return a string with applied whisper styles (colors, icons, labels) |
| `whisper_echo_set( String $message )` | Print the formatted message or route to drain if enabled |
| `whisper_echo_imbue( String $text )` | Apply all whisper formatting to the text (colors, icons, labels) |
| `whisper_call( String $prompt )` | Prompt user for input via terminal with styled message |
| `whisper_drain_start()` | Start buffering whisper output instead of printing directly |
| `whisper_drain_set( String $message )` | Store a line of whisper output into the drain buffer |
| `whisper_drain_get()` | Retrieve all buffered whisper output as a single string |
| `whisper_drain_end()` | Clear the whisper output buffer and disable buffering |
| `whisper_flash_start()` | init flash, reset pointer, start buffer |
| `whisper_flash_run()` | run one flash step, update pointer, flush output |
| `whisper_flash_stop()` | stop flash, end buffer, add newline |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `WHISPER` | main ether |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$WHISPER` | main essence |
| `$WHISPER_VARS` | Default text variables for whisper formatting (like newline, tab, etc.) |
| `$WHISPER_COLORS` | ANSI color codes for CLI output styling used by whisper |
| `$WHISPER_BG_COLORS` | ANSI background color codes for CLI output styling used by whisper |
| `$WHISPER_COLORS_WEBS` | HTML span-based color definitions for web-based whisper output |
| `$WHISPER_ICONS` | Default icon markers used in whisper output for each message type |
| `$WHISPER_LABELS` | Default label prefixes for whisper messages |
| `$WHISPER_DRAIN` | Buffer to store whisper output when in drain mode |
| `$WHISPER_DRAIN_STATE` | State toggle to determine whether whisper is in drain mode |

## Notes
- Style tokens: `{{nl}}` `{{tab}}` `{{bold}}` `{{end}}` `{{php}}`, and `{{color-X}}` `{{text-X}}` `{{bg-X}}` `{{icon-X}}` `{{label-X}}` where X is primary, secondary, success, warning, info, danger, error, failed, debug, default, end.
- Icons: `[√]` success · `[!]` warning · `[x]` danger/error/failed · `[i]` info · `[~]` primary · `[#]` secondary · `[^]` debug.
- Whisper's style values are not kept in the Weaver bond.

---
*Generated from `Whisper/Phantasm.php` (version 1.13). Read it live with `php cast grimoire --rune=Whisper`.*
