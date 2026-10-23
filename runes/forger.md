# Forger

> Built for structured file and directory operations such as tracing, scanning, fixing, moving, and cloning. Enables content analysis and automated organization through dynamic, logic-driven routines.

Forger shapes files and folders. It traces a path, fixes what is missing, writes and reads items, moves, clones, cleans, and watches a folder for change.

| | |
|---|---|
| **Version** | `1.14` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 1 · First Resonance |
| **Uses** | [Aether](aether.md) (entity), [Keeper](keeper.md) (entity) |
| **Awaken** | `use Rune\Forger\Manifest as Forger;` · `Forger::ether()::essence()::entity();` |

## When to use
- Make a path exist: `Forger::fix(Forger::trace($path))`.
- Write or read a file: `Forger::item($path, $text)` / `Forger::item($path)`.
- Remove a folder with everything inside: `Forger::clean($path, true)`.

## In code
```php
Chanter::cast('forge', function() {
  $box = AETHER_REPO . '/box';

  Forger::fix(Forger::trace($box . '/notes/hello.txt'));   // make missing folders and the file
  Forger::item($box . '/notes/hello.txt', 'Hello Rune');    // write
  Whisper::echo(Forger::item($box . '/notes/hello.txt') . '{{nl}}');   // read

  Forger::move([['type' => 'item', 'from' => $box . '/notes/hello.txt', 'target' => $box . '/copy.txt']]);   // copy a file
  foreach (Forger::scan($box) as $item) {
    Whisper::echo('- ' . $item['basename'] . '{{nl}}');
  }
  Whisper::echo('ext of copy.txt: ' . Forger::info($box . '/copy.txt')->ext . '{{nl}}');

  Forger::clean($box, true);   // remove the folder and everything inside
}, 'Make, read, copy and clean files.');
```

## Manifest
Call from your runite: `Forger::name(...)`.

| Method | Note |
|---|---|
| `_arise()` | *Legacy hook — not called by Aether.* |
| `_aether_end()` | *Legacy hook — not called by Aether.* |
| `end()` | Final phase of the class lifecycle, called after all manifest components are registered and ready. |
| `trace( String $source_path, ?Callable $callback = null )` | Traces and resolves each part of a given path, tagging them as file (item) or folder (repo) along with their existence. |
| `scan( String $source_path, ?Callable $callback = null )` | Scans a directory for items, applies a callback to each, and returns the result list. |
| `info( String $source_path )` | Retrieves detailed information about a file or directory, including type, basename, name, extension, and path. |
| `fix( Array $source_path )` | Ensures all given paths exist by creating missing directories or files based on their type. |
| `clean( String $source_path, bool $force = false )` | Cleans a file or directory; if forced as repo, recursively traces and removes all contained files and folders. |
| `move( Array $source_path )` | Moves or clones items and repositories to their target paths, ensuring destination structure exists beforehand. |
| `repo( string $source_path, bool $isRecursion = false )` | Ensures the repository path exists, fixes missing parts, and optionally scans items with a callback. |
| `item( string $source_path, Mixed $content = false, int $flags = 0 )` | Ensures the file exists, optionally writes content to it, and returns its contents. |
| `clone( string $from, string $to )` | Recursively clones a directory and its contents to a target location, creating folders as needed and copying files. |
| `observer( string $path )` | Observes a directory recursively and returns the latest modification timestamp among all files. |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `forger()` | Placeholder function for the Forger system, currently returns true. |
| `forger_trace( String $source_path, ?Callable $callback = null )` | Traces and resolves each part of a given path, tagging them as file ("item") or folder ("repo") along with their existence. |
| `forger_trace_recursive(string $path)` | Recursively traces a given path and all its children, returning structured info for both files and directories. |
| `forger_scan( String $source_path, ?Callable $callback )` | Scans a directory for items, applies a callback to each, and returns the result list. |
| `forger_fix( Array $source_path )` | Ensures all given paths exist by creating missing directories or files based on their type. |
| `forger_move(Array $source_path)` | Moves or clones items and repositories to their target paths, ensuring destination structure exists beforehand. |
| `forger_sort(array $trace, string $priority = "item")` | Sorts traced paths by type priority and path length, placing prioritized types first and longer paths earlier. |
| `forger_clean( String $source_path, $force_repo = false )` | Cleans a file or directory; if forced as repo, recursively traces and removes all contained files and folders. |
| `forger_repo(string $source_path, bool $isRecursion = false)` | Ensures the repository path exists, fixes missing parts, and optionally scans items with a callback. |
| `forger_item(string $source_path, mixed $content = false, int $flags = 0)` | Ensures the file exists, optionally writes content to it, and returns its contents. |
| `forger_info( String $source_path )` | Retrieves detailed information about a file or directory, including type, basename, name, extension, and path. |
| `forger_clone( string $from, string $to )` | Recursively clones a directory and its contents to a target location, creating folders as needed and copying files. |
| `forger_observer($path)` | Observes a directory recursively and returns the latest modification timestamp among all files. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `FORGER` | main ether |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$FORGER` | main essence |
| `$FORGER_KEEPER_SHARD` | Whether files written by Forger are kept as shards by Keeper. |

## Notes
- `item` = file, `repo` = folder.
- `Forger::move()` copies: an `item` is copied, a `repo` is cloned. Clean the source yourself to move.
- `Forger::item()` writes only when the folder exists; use `fix` first.
- While Keeper is awake, files written by Forger are added to the shard list (`FORGER_KEEPER_SHARD`).

---
*Generated from `Forger/Phantasm.php` (version 1.14). Read it live with `php cast grimoire --rune=Forger`.*
