# Aether

> Represents the foundational flow that permeates all components—serves as the invisible layer connecting, powering, and synchronizing every part of the system.

Aether is the flow that runs beneath everything. It is the first rune to awaken and the last one to rest: it opens the flow, measures its time and memory, records every step as **arcane**, and closes the flow with the version footer.

| | |
|---|---|
| **Version** | `1.18` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 0 · The Void |
| **Uses** | [Chanter](chanter.md) (entity), [Whisper](whisper.md) (entity) |
| **Awaken** | `use Rune\Aether\Manifest as Aether;` · `Aether::ether()::essence()::entity();` |

## When to use
- Every runite begins with `Aether::begin()` and ends with `Aether::end()`.
- Ask about the flow: time (`aether_stopwatch`), memory (`aether_memoryusage`), what is awake (`aether_has_entity`, `aether_arised`).
- Debug with `Aether::dd($data)`.

## In code
```php
Chanter::cast('flow', function() {
  [$usage, $peak] = aether_memoryusage();

  Whisper::echo('Runite  ' . AETHER_FILE . ' in ' . AETHER_REPO . '{{nl}}');
  Whisper::echo('Time    ' . number_format(aether_stopwatch(), 4) . 's{{nl}}');
  Whisper::echo('Memory  ' . aether_formatFileSize($usage) . ' (peak ' . aether_formatFileSize($peak) . '){{nl}}');
  Whisper::echo('Keeper  ' . (aether_has_entity('keeper') ? 'awake' : 'asleep') . '{{nl}}');
  Whisper::echo('Runes   ' . implode(', ', aether_list_runes()) . '{{nl}}');
}, 'Show the flow of this runite.');
```

## Manifest
Call from your runite: `Aether::name(...)`.

| Method | Note |
|---|---|
| `begin( $flags = 0 )` | Begins the Aether flow: cleans memory and resets arcane. |
| `end()` | Ends the Aether flow and exits with the version footer. |
| `dd( $data, $force=false  )` | Dumps data and stops the flow. |
| `exit( $force = false )` | Exits the flow now with the version footer. |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `aether_formatFileSize($size, $precision = 2)` | Convert a number of bytes into a human-readable file size (e.g. KB, MB) |
| `aether_stopwatch()` | Measure elapsed time since $AETHER_STOPWATCH was started (in seconds) |
| `aether_memoryusage()` | Get current and peak memory usage in bytes |
| `aether_zero_trust( Mixed $state = "" )` | Gets or sets the zero-trust state of the flow. |
| `aether_exit( $force = false )` | Exit the program with execution time and memory usage summary (supports pretty output with whisper) |
| `aether_has_entity( $function )` | Check if a given function (entity) exists in the current environment |
| `aether_has_ether( $rune )` | Check if a constant (ether) is defined in the runtime |
| `aether_has_essence( $rune )` | Check if a global variable (essence) is set and exists |
| `aether_dd( $data, $force=false )` | Dump and display debug information with colorized formatting, then exit |
| `aether_whisper( $text )` | Prints text without Whisper (style tokens removed). |
| `aether_whisper_echo( $text )` | Echoes through Whisper when awakened, otherwise prints plain text. |
| `aether_arised()` | Get all unique arised runes from ether, essence, and entity |
| `aether_arcane(String $text, String $value = "")` | Track execution events with timestamp and elapsed time (arcane trace logging) |
| `aether_arcane_old(String $text, String $value = "")` | Old arcane recorder (kept for reference). |
| `aether_arcane_reset()` | Reset all arcane trace logs |
| `aether_arcane_enable()` | Enable arcane trace logging |
| `aether_arcane_disable()` | Disable arcane trace logging |
| `aether_arcane_pretty_print()` | Prints the arcane records of this flow (development). |
| `aether_version( Bool $all = false )` | Version of Rune: &lt;major AETHER_VERSION&gt;.&lt;minor AETHER_VERSION + sum of rune majors&gt;.&lt;sum of rune minors&gt;, read as integers; $all adds liberation runes. |
| `aether_list_runes()` | Lists origin runes plus @liberations runes in liberation mode. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `AETHER` | Flag that the Aether flow is active. |
| `AETHER_FILE` | The runite being cast, as it was typed (e.g. cast, realm/cast). |
| `AETHER_REPO` | The folder of the runite itself, wherever it is cast from (falls back to getcwd). |
| `AETHER_VERSION` | Version of the Rune core. |
| `AETHER_COPYRIGHT` | Copyright line placed in crafted and artefact output. |
| `AETHER_RUNE_LOCATION` | Folder of the origin runes. |
| `AETHER_SELF_WEAVER` | Folder of Aether"s own weaver templates. |
| `AETHER_LOGS` | Legacy logs folder inside .echoes (kept for old runites). |
| `AETHER_ECHOES` | The .echoes folder of the working folder. |
| `AETHER_ECHOES_RUNE` | Legacy echoes folder of the runite (Keeper now keeps the echoes). |
| `AETHER_ECHOES_INFORMATION` | Legacy information file of the runite echoes. |
| `AETHER_ECHOES_ARCANE` | Legacy arcane file of the runite echoes. |
| `AETHER_ECHOES_ARCANES` | Legacy arcanes file of the runite echoes. |
| `AETHER_ECHOES_ARTEFACT` | Legacy artefact folder of the runite echoes. |
| `AETHER_PHP_VERSION` | PHP version the Rune core was built with. |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$AETHER_STOPWATCH` | Start time of the flow, used for the Execute time. |
| `$AETHER_ARCANE_STOPWATCH` | Start time used to measure arcane steps. |
| `$AETHER_ARCANE_STOPWATCH_STEP` | Time of the last arcane step. |
| `$AETHER_RUNE` | Runes awakened in this flow. |
| `$AETHER_RUNE_ETHER` | Runes whose ether is awakened. |
| `$AETHER_RUNE_ESSENCE` | Runes whose essence is awakened. |
| `$AETHER_RUNE_ENTITY` | Runes whose entity is awakened. |
| `$AETHER_RUNE_MANIFEST` | Runes whose manifest is awakened. |
| `$AETHER_RUNE_PHANTASM` | Phantasm of the awakened runes. |
| `$AETHER_ZERO_TRUST` | Zero-trust state (output drained, arcane disabled). |
| `$AETHER_ARCANE` | Arcane records of this flow. |
| `$AETHER_ARCANE_STATE` | Whether arcane is recorded (enable/disable). |

## Notes
- `aether_list_runes()` lists the ten origin runes, plus the runes in `@liberations/` when the runite is in liberation mode. `aether_version()` adds their Phantasm versions as whole numbers: `<major AETHER_VERSION>.<minor AETHER_VERSION + rune majors>.<rune minors>`. The footer `Version=` counts liberation runes too; the release counts origin runes only.
- `AETHER_REPO` is the runite's own folder, wherever it is cast from, and `AETHER_FILE` the runite as typed (`cast`, `realm/cast`).
- Constants `AETHER_LOGS`, `AETHER_ECHOES_RUNE`, `AETHER_ECHOES_INFORMATION`, `AETHER_ECHOES_ARCANE(S)`, `AETHER_ECHOES_ARTEFACT` are legacy — Keeper owns the echoes now.

---
*Generated from `Aether/Phantasm.php` (version 1.18). Read it live with `php cast grimoire --rune=Aether`.*
