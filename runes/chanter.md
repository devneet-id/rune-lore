# Chanter

> Encapsulates processes and CLI-style operations to maintain immutability—structures input, spell logic, and execution flow into controlled, traceable, and reusable command definitions.

Chanter is the gate of the command line. A **cast** is a command, a **spell** is its option, and an **echo** is the note shown on the main screen.

| | |
|---|---|
| **Version** | `1.14` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 0 · The Void |
| **Uses** | [Aether](aether.md) (entity), [Whisper](whisper.md) (entity), [Specter](specter.md) (entity) |
| **Awaken** | `use Rune\Chanter\Manifest as Chanter;` · `Chanter::ether()::essence()::entity();` |

## When to use
- Register: `Chanter::cast('greet --name', fn, 'Greet someone.')`.
- Read a spell: `Chanter::spell('name')` — `false` when missing, `'1'` when given without a value.
- Cast from code: `Chanter::cast('greet --name=Rune')()` returns the cast's return value.

## In code
```php
// php cast greet --name=Anwar --loud
Chanter::cast('greet --name --loud', function() {
  $name = Chanter::spell('name');
  if (!$name || $name === '1') {
    $name = 'traveler';        // a spell without a value is '1'
  }
  $text = "Hello, $name!";
  Whisper::echo((Chanter::spell('loud') ? strtoupper($text) : $text) . '{{nl}}');
  return $text;
}, 'Greet someone. --name=<name> --loud');

// a cast can cast another cast, and get its return value
Chanter::cast('greet-twice', function() {
  $first = Chanter::cast('greet --name=Rune')();
  Chanter::cast('greet --name=Rune --loud')();
  return $first;
}, 'Cast greet two times.');
```

## Manifest
Call from your runite: `Chanter::name(...)`.

| Method | Note |
|---|---|
| `begin()` | Begins Chanter: loads the built-in casts from @bindrune/chanter. |
| `end()` | Prepares and executes a spell casting based on provided arguments or from file. |
| `cast( String $arg, ?Callable $execute = NULL, String $echo = "" )` | Gets or sets a spell cast definition based on input and returns the result. |
| `spell( String $key, Mixed $value = NULL, Mixed $fail = false )` | Gets or sets a spell definition by key and returns the result. |
| `echo( String $arg, String $note = "" )` | Outputs the given text and returns it |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `chanter()` | Main entity |
| `chanter_arg( String $newArg = "" )` | Sets or returns the current CLI argument string |
| `chanter_arg_extract( String $newArg = "" )` | Parses CLI arguments into cast parts and spell options |
| `chanter_arg_rebase()` | Checks if a specific spell name exists in the global $CHANTER_ARG_SPELL array and its value is not equal to |
| `chanter_cast( String $args, ?Callable $callable )` | Gets or registers a cast function based on the given arguments. |
| `chanter_cast_set( String $arg, ?Callable $callable )` | Registers a new cast if it doesn’t already exist in the cast list. |
| `chanter_cast_get( String $arg )` | Returns a registered cast function or a fallback if not found |
| `chanter_cast_has( String $arg )` | Checks if a cast function exists for the given arguments |
| `chanter_spell( String $name, $values = NULL )` | Gets or sets a spell by name depending on whether values are provided |
| `chanter_spell_set( String $name, String $value )` | Registers or updates a spell with the given name and value |
| `chanter_spell_get( String $name )` | Retrieves the value of a spell argument if it exists |
| `chanter_spell_chain()` | Builds a full CLI-style spell string from all current spell arguments |
| `chanter_spell_has( String $name )` | Checks whether a spell is given with a value (not only as a flag) |
| `chanter_echo_name( String $arg )` | Takes the cast name from a cast signature (`quest --add --rank` -&gt; `quest`) |
| `chanter_echo_set( String $arg, String $notes )` | Adds notes to the echo data if the entry doesn’t exist yet. |
| `chanter_echo_get( String $arg )` | Retrieves the echo data for a given cast argument |
| `chanter_whisper_drain( $run )` | Runs a cast while draining Whisper output, then echoes it at once (zero-trust). |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `CHANTER` | Main ether |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$CHANTER` | Main essence |
| `$CHANTER_ARG` | Stores full CLI argument string as a single line |
| `$CHANTER_ARGS` | Stores full CLI argument string as an array |
| `$CHANTER_ARG_CAST` | Holds parsed cast-related arguments from CLI |
| `$CHANTER_ARG_SPELL` | Contains full list of separated CLI arguments |
| `$CHANTER_ARG_LIST` | Contains full list of separated CLI arguments |
| `$CHANTER_CAST` | Stores all available cast definitions |
| `$CHANTER_CAST_LIST` | List of registered cast names or keys |
| `$CHANTER_SPELL` | Spells set from code (Chanter::spell(key, value)), read on the next cast. |
| `$CHANTER_ECHO` | Holds text or data to be echoed after cast execution |

## Notes
- `Chanter::begin()` loads the built-in casts (rune, grimoire, sentinel, artefact); `Chanter::end()` runs the cast asked on the command line.
- Spell values keep `0` and `+`; use quotes or `%20` for spaces.
- A spell set from code (`Chanter::spell('x', 'v')`) is read on the next cast — by design.
- `--zero-trust` runs the cast with the arcane off and the output drained.
- Known issue: `chanter_cast_has()` always returns false.

---
*Generated from `Chanter/Phantasm.php` (version 1.14). Read it live with `php cast grimoire --rune=Chanter`.*
