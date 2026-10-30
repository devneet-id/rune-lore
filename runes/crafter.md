# Crafter

> Focused on dynamic creation and composition—designed to build, shape, and assemble various data structures or logic units through modular, seed-based, and spark-driven processes.

Crafter is the builder. An **item** is what you craft, its **seed** is the recipe, its **shards** are the source files, and the **spark** bundles them into one distributable file.

| | |
|---|---|
| **Version** | `1.13` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 2 · Understanding Its Flow |
| **Uses** | [Aether](aether.md) (ether), [Cipher](cipher.md) (entity), [Forger](forger.md) (essence:entity), [Weaver](weaver.md) (entity), [Whisper](whisper.md) (entity) |
| **Awaken** | `use Rune\Crafter\Manifest as Crafter;` · `Crafter::ether()::essence()::entity();` |

## When to use
- Describe: `Crafter::item('site', fn)` with `Crafter::seed(...)` and `Crafter::shard(...)` inside.
- Build: `Crafter::spark('site')`.

## In code
```php
// src/index.html, src/index.css, src/index.js, src/index.php → dist/index.php
Chanter::cast('build', function() {
  Crafter::item('site', function() {
    Crafter::seed('DIST', AETHER_REPO . '/dist/index.php');
    Crafter::seed('TYPE', 'plain');
    Crafter::seed('LANGUAGE', ['html', 'css', 'js', 'php']);
    Crafter::shard('src/index.html');
    Crafter::shard('src/index.css');
    Crafter::shard('src/index.js');
    Crafter::shard('src/index.php');
  });
  Crafter::spark('site');
}, 'Bundle src/ into dist/index.php.');
```

## Manifest
Call from your runite: `Crafter::name(...)`.

| Method | Note |
|---|---|
| `item(string $name, ?callable $callable = null)` | Registers or retrieves a crafter item by name; sets the active name if callable is provided. |
| `seed(string $name, mixed $value = null)` | Sets or retrieves a value from the crafter seed configuration. |
| `shard(string $source, ?callable $injection = null)` | Retrieves or registers a shard source with optional injection logic. |
| `spark(mixed $name_or_callable = null, ?callable $injection = null)` | Executes the full crafting process using item name or callable, then resets the crafter state and shows crafting summary. |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `crafter()` | Main entity. |
| `crafter_reset()` | Reset all Crafter globals to initial states using constants or empty values. |
| `crafter_seed_set(String $name, Mixed $value)` | Store a value into the global CRAFTER_SEED array using the given name as key. |
| `crafter_seed_get(String $name)` | Get a value from the global CRAFTER_SEED array using the given name as key. |
| `crafter_item_set(String $name, ?Callable $callable)` | Register a callable into the global CRAFTER_ITEM array using the given name as key. |
| `crafter_item_get(String $name)` | Execute a registered crafter item callable by name and update CRAFTER_SPARK with current state. |
| `crafter_shard_set(String $file_path, ?Callable $injection = NULL)` | Register a shard file with optional injection, and store its info and path in global shard arrays. |
| `crafter_shard_get(String $file_path, ?Callable $injection = NULL)` | Retrieve a shard file info, registering it first if not already listed. |
| `crafter_spark(String $name, ?Callable $injection = NULL)` | Run full crafting pipeline — validate readiness, process shards, apply injection, and finalize crafting result. |
| `crafter_spark_message()` | Display crafting summary with item name, output path, file size, and total shards used. |
| `crafter_spark_clustering()` | Inject and group each shard’s content into the appropriate cluster based on name or file type. |
| `crafter_spark_cleaning()` | Clean each cluster by removing unwanted patterns using language-specific cleaning rules. |
| `crafter_spark_bundling()` | Bundle cleaned shard clusters and metadata into a final distributable template. |
| `crafter_spark_distributing()` | Write the bundled template to the distribution path defined in crafter seed. |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `CRAFTER` | Flag to enable or indicate the Crafter system is active. |
| `CRAFTER_WEAVER` | Defines available weaver templates for different language sets and output types (plain, class, function), used during bundling. |
| `CRAFTER_VARIABLE` | Maps cluster types to variable placeholders used during template binding. |
| `CRAFTER_CLEANING` | Defines cleaning rules for each language type to remove unwanted wrappers or tags before bundling. |
| `CRAFTER_RESET_SEED` | Default seed configuration used when resetting the Crafter state. |
| `CRAFTER_RESET_SPARK` | Default empty structure for CRAFTER_SPARK used during reset. |
| `CRAFTER_RESET_SPARK_STATE` | Default spark state, marking the crafter as not ready after reset. |
| `CRAFTER_RESET_SPARK_CLUSTER` | Default empty cluster groups for each language type after reset. |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$CRAFTER` | Main flag to indicate that the Crafter system is active. |
| `$CRAFTER_ITEM` | Stores registered crafter items as callable functions. |
| `$CRAFTER_SEED` | Stores registered crafter items as callable functions. |
| `$CRAFTER_SHARD` | Holds processed shard info from files. |
| `$CRAFTER_SHARD_LIST` | List of shard file paths to be processed. |
| `$CRAFTER_SHARD_INJECTION` | Injection callbacks associated with shard file paths. |
| `$CRAFTER_SPARK` | Stores crafting metadata including selected item, seed data, and loaded shards. |
| `$CRAFTER_SPARK_STATE` | State flags for the crafting process, such as readiness. |
| `$CRAFTER_SPARK_CLUSTER` | Clustered content grouped by type, used during bundling (e.g., html, css, js, etc). |
| `$CRAFTER_SPARK_DISTRIBUTE` | Final crafted content ready to be written to output. |

## Notes
- Seeds: `DIST` (output file), `TYPE` (`plain`, `class`, `function`), `LANGUAGE` (`html`, `css`, `js`, `php`), `MINIFIED`, `ENCRYPTION` (`base64`).
- A shard named `*.head.html` goes into `<head>`.
- Templates live in `Crafter/weaver/`.
- Crafter is the door to **Exura**, the simple toolkit for websites.

---
*Generated from `Crafter/Phantasm.php` (version 1.13). Read it live with `php cast grimoire --rune=Crafter`.*
