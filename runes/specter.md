# Specter

> Enables out-of-process operations through soul-like abstractions—designed for managing complex, asynchronous, or decoupled executions by temporarily separating logic from the main flow while maintaining active control.

Specter works beyond the main flow. It keeps a **soul** that outlives a run, casts commands in another window, watches with the **seer**, observes folders, and starts a development server.

| | |
|---|---|
| **Version** | `1.9` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 3 · Liberation of Forte |
| **Uses** | [Keeper](keeper.md) (ether), [Aether](aether.md) (ether), [Weaver](weaver.md) (entity), [Forger](forger.md) (entity), [Whisper](whisper.md) (entity) |
| **Awaken** | `use Rune\Specter\Manifest as Specter;` · `Specter::ether()::essence()::entity();` |

## When to use
- Soul: `Specter::soul('name', $value)` / `Specter::soul('name')`.
- Another window: `Specter::cast('{{self}} serve', ['visible' => true])`.
- Dev server: `Specter::devserver(['port' => 8000, 'file' => ...])`.

## In code
```php
Chanter::cast('soul --name --value', function() {
  $name = Chanter::spell('name') ?: 'mood';
  $value = Chanter::spell('value');
  if ($value && $value !== '1') {
    Specter::soul($name, $value);                         // .echoes/<runite>/soul.json
  }
  Whisper::echo("$name = " . (Specter::soul($name) ?? '(empty)') . '{{nl}}');
}, 'Keep a soul value. --name=mood --value=calm');

// open another terminal window and run a cast of this runite there
Chanter::cast('beside', function() {
  Specter::cast('{{self}} soul --name=mood', ['visible' => true]);
}, 'Run a cast in another window.');
```

## Manifest
Call from your runite: `Specter::name(...)`.

| Method | Note |
|---|---|
| `_arise()` | *Legacy hook — not called by Aether.* |
| `_aether_end()` | *Legacy hook — not called by Aether.* |
| `end()` | Final phase of the class lifecycle, called after all manifest components are registered and ready. |
| `observer( $repo, $callback )` | Start observing changes in a directory and trigger callback on modification |
| `devserver( $configure )` | Launch a local PHP development server with configurable host, port, and router |
| `soul( String $name, Mixed $value = NULL )` | Store or retrieve a named soul value (persistent memory) |
| `cast( String $arg, Array $options = [] )` | Register or run a terminal command cast with optional behavior settings |
| `seer( ?Callable $callback )` | Start a visual loop animation until a stop condition or glitch is met |
| `exit( String $arg )` | Mark a previously casted command as inactive (used to exit the cast lifecycle) |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `specter()` | main entity |
| `specter_soul_set( String $name, Mixed $value )` | Sets a soul value and persists it through the keeper. |
| `specter_soul_get( String $name )` | Retrieves a soul value and refreshes the in-memory state. |
| `specter_soul_save( $name, $value = null )` | Loads and syncs soul data from keeper, optionally updates a value. |
| `specter_soul_remove( String $name )` | Removes a soul value from both memory and keeper storage. |
| `specter_cast_set( string $arg, array $options = [] )` | Executes a command with given options across platforms and logs the cast state. |
| `specter_cast_get( string $arg )` | Retrieves cast state by argument from keeper storage. |
| `specter_cast_save( $arg, $alive = true, $option = [] )` | Saves the cast command and its metadata to keeper storage. |
| `specter_seer_set(?Callable $condition)` | Continuously calls a condition callback with spinner frames until stopped or glitch is detected. |
| `specter_exit( String $arg )` | Marks a casted specter command as no longer active. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `SPECTER` | main ether |
| `SPECTER_ECHOES_SOUL` | Path to the file where Specter soul data (state/configuration) is stored. |
| `SPECTER_ECHOES_CAST` | Path to the file where Specter cast data (execution history/config) is stored. |
| `SPECTER_CAST_DEFAULT` | Default structure for a Specter cast, indicating execution state and options. |
| `SPECTER_CAST_ARG_DEFAULT` | Default command-line options for Specter cast executions. |
| `SPECTER_SEER_OPTION` | Default configuration for Specter Seer, mainly controlling loop speed and delays. |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$SPECTER` | main essence |
| `$SPECTER_ITEMS` | Holds the list of all registered Specter items. |
| `$SPECTER_STATS` | Stores runtime statistics for Specter items. |
| `$SPECTER_SOUL` | Stores the soul data of the Specter, usually persistent state or configuration. |
| `$SPECTER_CAST` | Contains casting records and arguments used when Specter runs external processes. |

## Notes
- `{{self}}` becomes `php <runite>`.
- Visible casts open `cmd` on Windows, Terminal on macOS, `gnome-terminal` on Linux.
- The soul lives in `.echoes/<runite>/soul.json`, so Keeper must be engraved.

---
*Generated from `Specter/Phantasm.php` (version 1.9). Read it live with `php cast grimoire --rune=Specter`.*
