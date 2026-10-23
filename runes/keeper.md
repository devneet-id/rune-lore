# Keeper

> Handles persistent message tracking, data logging, and structured memory management—acts as a system-level manager for recording, retrieving, and organizing information across operations.

Keeper is the memory of a runite. It keeps **echoes** in `.echoes/<runite>/`: items, shards, the arcane of every run, and the **glitch** when something breaks.

| | |
|---|---|
| **Version** | `1.12` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 1 · First Resonance |
| **Uses** | [Aether](aether.md) (ether), [Chanter](chanter.md) (entity), [Cipher](cipher.md) (entity), [Forger](forger.md) (entity), [Specter](specter.md) (entity), [Whisper](whisper.md) (entity) |
| **Awaken** | `use Rune\Keeper\Manifest as Keeper;` · `Keeper::ether()::essence()::entity();` |

## When to use
- Engrave it: `Keeper::begin()` after `Chanter::begin()`, and `Keeper::end()` before `Aether::end()`.
- Remember: `Keeper::item('name', $data)` / `Keeper::item('name')` (an object).
- Carry files into an artefact: `Keeper::shard(['folder', 'file.txt'])`.

## In code
```php
// Keeper needs Keeper::begin() after Chanter::begin() and Keeper::end() before Aether::end()
Chanter::cast('remember --text', function() {
  $text = Chanter::spell('text');
  if ($text && $text !== '1') {
    Keeper::item('memory', ['text' => $text]);          // .echoes/<runite>/memory.json
  }
  $memory = Keeper::item('memory');                       // an object, or null
  Whisper::echo('memory: ' . ($memory->text ?? '(empty)') . '{{nl}}');
  Whisper::echo('kept in ' . KEEPER_ECHOES . '{{nl}}');
}, 'Remember a text in .echoes. --text="..."');
```

## Manifest
Call from your runite: `Keeper::name(...)`.

| Method | Note |
|---|---|
| `begin( $flags = 0 )` | Special hook for aether-based awakening phase, executed at the start of the crafter process. |
| `end()` | Final phase of the class lifecycle, called after all manifest components are registered and ready. |
| `echo( String $repo, String $name, $value = "" )` | Reads or writes a raw file inside the given repo depending on value. |
| `item( String $name, $value = false )` | Gets or sets a structured keeper item in JSON format. |
| `shard(Array\|String $source)` | Saves rune shard(s) from string or array source. |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `keeper()` | Main entity |
| `keeper_arcane_process()` | Converts arcane log entries into a readable format with timing and state evaluation, then stores the result. |
| `keeper_arcane_process_store( $datas )` | Saves processed arcane log data into a timestamped file. |
| `keeper_item( String $name, $value = "" )` | Gets or sets a keeper item based on whether a value is provided. |
| `keeper_item_set( String $name, $value )` | Saves a value as a formatted JSON file under the given name. |
| `keeper_item_get( String $name )` | Retrieves and decodes a JSON file by name into a usable value. |
| `keeper_echo( String $repo, String $name, $value = "" )` | Reads or writes a raw file inside a given repository, depending on whether a value is provided. |
| `keeper_echo_set( String $repo, String $name, $value )` | Ensures the target repository exists, then saves the given value as a plain file. |
| `keeper_echo_get( String $repo, String $name )` | Reads and returns the contents of a plain file from the given repository. |
| `keeper_shard_set( String $source_path )` | Traces files, collects valid items, and stores them as encoded rune shards. |
| `keeper_shard_set_all( Array $file_maps )` | Adds many files and folders to the shard list at once. |
| `keeper_shard_clean()` | Cleans all stored shards and resets the shard repository. |
| `keeper_glitch_boot()` | Initializes custom error, exception, and shutdown handlers to capture and log all glitches into a file. |
| `keeper_glitch_message( $glitch )` | Shows the glitch screen (severity, line, file, message). |
| `keeper_glitch_detect()` | Dumps the current glitch state for inspection. |
| `keeper_is_glitch()` | Checks if the glitch log file has content, indicating an error has occurred. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `KEEPER` | main ether |
| `KEEPER_ECHOES` | Base directory for all Keeper-related output files and logs. |
| `KEEPER_ECHOES_KEEPER` | Path to the main keeper state file. |
| `KEEPER_ECHOES_STATS` | Path to the statistics log file for tracking system data. |
| `KEEPER_ECHOES_ARCANE` | Path to the active arcane log file containing process entries. |
| `KEEPER_ECHOES_GLITCH` | Path to the glitch log file for captured errors and exceptions. |
| `KEEPER_ECHOES_ARCANES` | Directory for archived arcane logs. |
| `KEEPER_ECHOES_SHARDS` | Directory for encoded shard backups. |
| `KEEPER_ECHOES_SHARD` | Shard list of the runite (files carried into the artefact). |
| `KEEPER_SAVING_ECHOES` | Flag bit for Keeper::begin(): save echoes. |
| `KEEPER_SHOW_GLITCH` | Flag bit for Keeper::begin(): show glitch screen. |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$KEEPER` | main essence |
| `$KEEPER_ARCANE` | Defines stepwatch thresholds for classifying performance stages in arcane processing (e.g., BURST to OVERCLOCK). |
| `$KEEPER_SAVING_ACTIVE` | Whether Keeper is saving echoes in this flow. |

## Notes
- Without `Keeper::begin()` the `.echoes` folder does not exist and `Keeper::item()` saves nothing (it still returns `true`). `sentinel --invoke=Keeper` does not add `begin`/`end` for you.
- Every runite has its own folder: `.echoes/cast/`, `.echoes/ember/`…
- Arcane states by step time: BURST, FLASH, FLOW, FALL, BREAK, COLLAPSE, OVERCLOCK.
- Known issue: writing with `Keeper::echo()` glitches; read works.

---
*Generated from `Keeper/Phantasm.php` (version 1.12). Read it live with `php cast grimoire --rune=Keeper`.*
