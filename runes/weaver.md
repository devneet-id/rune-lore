# Weaver

> Built for advanced string manipulation, data binding, and template weaving—transforming raw data into structured text with flexible, context-aware logic.

Weaver turns raw data into text. It binds values into `{{tokens}}`, remembers them in the **bond**, loads templates, wraps long lines, and minifies HTML, CSS, JS and PHP.

| | |
|---|---|
| **Version** | `1.7` |
| **Mark** | `VOID` |
| **By** | Anwar Achilles |
| **Introduced in** | Act 0 · The Void |
| **Uses** | [Aether](aether.md) (entity) |
| **Awaken** | `use Rune\Weaver\Manifest as Weaver;` · `Weaver::ether()::essence()::entity();` |

## When to use
- Bind: `Weaver::bind($template, ['name' => 'Anwar'])`.
- Load a template file once: `Weaver::item(__DIR__ . '/card.txt')`.
- Read a remembered value: `Weaver::bond('name', null)`.

## In code
```php
Chanter::cast('weave', function() {
  // bind one value, or many at once
  $card = Weaver::bind('{{who}} casts {{spell}}', ['who' => 'Anwar', 'spell' => 'fire']);
  Whisper::echo($card . '{{nl}}');

  // every bound value is kept in the bond
  Whisper::echo('bond who = ' . Weaver::bond('who', null) . '{{nl}}');

  // wrap a long text by word
  Whisper::echo(weaver_wrap_word('Rune is a lore-driven, modular concept beneath PHP.', 20) . '{{nl}}');

  // minify
  Whisper::echo(weaver_min('body {  color : red ; }', 'css') . '{{nl}}');
}, 'Weave text from templates.');
```

## Manifest
Call from your runite: `Weaver::name(...)`.

| Method | Note |
|---|---|
| `_arise()` | *Legacy hook — not called by Aether.* |
| `_aether_end()` | *Legacy hook — not called by Aether.* |
| `end()` | Final phase of the class lifecycle, called after all manifest components are registered and ready. |
| `bind( String $template, $searchOrArray, String $data="" )` | Bind one or multiple variables into a template string |
| `bond( String $key, Mixed $value )` | Set or retrieve a key-value bond for template variable storage |
| `item( String $source, String $alias="" )` | Load a template file into memory and optionally assign it an alias |

## Entity
The logic. Other runes call these functions too.

| Function | Note |
|---|---|
| `weaver()` | main entity |
| `weaver_wrap_echo($text, $wrap, $divider)` | Wrap and prefix text lines with a divider for formatted echo output |
| `weaver_wrap_word($text, $wrap = 50, $divider = "", $cutFirst = false)` | wraps text by word length using space as word boundary |
| `weaver_wrap_letter($text, $wrap = 50, $divider = "", $cutFirst = false)` | wraps text by exact letter count without word boundary |
| `weaver_bind( $template, $search, String $data = "", Bool $bond = true )` | Replace a variable placeholder in a template with given data |
| `weaver_bind_extract( $value )` | Extract all variable placeholders from a template string |
| `weaver_bind_multiple( $template, $datas, Bool $bond = true )` | Bind multiple placeholders in a template using key-value data |
| `weaver_bond_combine( $datas )` | Merge and store new template data into the global weaver bond |
| `weaver_bond_set( $key, $value )` | Set a single key-value pair into the global weaver bond |
| `weaver_bond_get( $key )` | Get a stored value from the global weaver bond using its key |
| `weaver_item( $source, $datas = [] )` | Load and bind a template file with dynamic data replacements |
| `weaver_item_set( $source, $alias = "" )` | Load a template file and store it in memory, optionally using an alias |
| `weaver_item_get( $find_source_alias )` | Retrieve a stored template from memory by its alias or file path |
| `weaver_min( $input, $type="html" )` | Minify content by removing whitespace, comments, and unnecessary characters |
| `weaver_min_css( $input )` | Minify CSS content by removing whitespace, comments, and unnecessary characters |
| `weaver_min_js( $input )` | Minify JavaScript content by stripping out whitespace and simplifying expressions |
| `weaver_min_html($input)` | Minify HTML content by collapsing spaces and removing unnecessary tags or breaks |
| `weaver_min_php($input)` | Minify PHP code by trimming extra whitespace and cleaning up the syntax |

## Ether
Constants — truth that never changes.

| Constant | Note |
|---|---|
| `WEAVER` | main ether |

## Essence
Globals — state that changes as the flow goes on.

| Global | Note |
|---|---|
| `$WEAVER` | main essence |
| `$WEAVER_BOND` | Global storage for bound template variables (key-value pairs) |

## Notes
- A token matches in lower case or upper case (`{{name}}` and `{{NAME}}`), not in mixed case.
- Every bind is remembered in the bond. To bind values for one use only, call `weaver_bind_multiple($template, $data, false)`.
- `Weaver::bond()` needs its second argument: pass `null` to read.
- Known issue: `weaver_item($file, [...])` with data glitches; bind the result with `Weaver::bind()` instead.

---
*Generated from `Weaver/Phantasm.php` (version 1.7). Read it live with `php cast grimoire --rune=Weaver`.*
