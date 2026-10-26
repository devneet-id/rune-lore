# Crafter

> The builder: describe an item, then spark it.

<!-- status: draft -->

Crafter is the forge of Rune. You describe what to build — an **item** with its **seed** (the recipe) and its **shards** (the source files). Then you **spark** it, and many files become one.

## The words

| Word | Is | Call |
|---|---|---|
| **item** | what you build, by name | `Crafter::item('page', fn)` |
| **seed** | the recipe: where, what kind, which languages | `Crafter::seed('DIST', $path)` |
| **shard** | one source file | `Crafter::shard('src/index.html')` |
| **spark** | build it now | `Crafter::spark('page')` |

## In code

Awaken Crafter with the runes it leans on — Forger, Weaver, Cipher, Whisper (see [Runes Lean on Runes](runes-lean-on-runes.md)).

```php
use Rune\Crafter\Manifest as Crafter;
// ...
Crafter::ether()::essence()::entity();

Chanter::cast('build', function() {
  Crafter::item('page', function() {
    Crafter::seed('DIST', AETHER_REPO . '/dist/index.html');
    Crafter::seed('TYPE', 'plain');
    Crafter::seed('LANGUAGE', ['html', 'css', 'js']);
    Crafter::seed('MINIFIED', ['css', 'js']);
    Crafter::shard('src/index.head.html');
    Crafter::shard('src/index.html');
    Crafter::shard('src/index.css');
    Crafter::shard('src/index.js');
  });
  Crafter::spark('page');
}, 'Bundle src/ into dist/index.html.');
```

```
$ php cast build
[√] Crafting page has been Sparked!!
[i]INFO: Path=/.../dist/index.html, Size=345.00B, Shard=4
```

The item's callable runs only when it is sparked.

## Seeds

| Seed | Default | Meaning |
|---|---|---|
| `DIST` | — (**required**) | the output file; its folder is made for you |
| `TYPE` | `class` | `plain`, `function` or `class` |
| `LANGUAGE` | `['html', 'css', 'js', 'php']` | the languages of the shards — must match a template (below) |
| `MINIFIED` | `[]` | languages to minify with Weaver, e.g. `['css', 'js']` |
| `ENCRYPTION` | `base64` | how `function` and `class` hide their source |

`CHARSET`, `LINT` and `REPO` also exist in the seed but are not used yet.

## Templates — which `TYPE` + `LANGUAGE`

The template is chosen by **exact** match, order included:

| `TYPE` | `LANGUAGE` | Result |
|---|---|---|
| `plain` | `['html', 'css', 'js', 'php']` | a `.php` page: PHP on top, then HTML with `<style>` and `<script>` |
| `plain` | `['html', 'css', 'js']` | an `.html` page |
| `plain` | `['css']` | one CSS file |
| `plain` | `['js']` | one JS file |
| `plain` | `['php']` | one PHP file |
| `function` | `['html', 'css', 'js', 'php']` | a PHP file that rebuilds and runs the page from base64 inside functions |
| `class` | `['html', 'css', 'js', 'php']` | the same, inside a class |

Anything else has no template and glitches: `Undefined variable $templates`. The templates live in `Crafter/weaver/`.

## Shards

- A shard is a path, read relative to where you run the runite. A missing file is skipped.
- Its **extension** decides its cluster: `.html`, `.css`, `.js`, `.php`.
- A name with `.head` (e.g. `index.head.html`) goes into `<head>` instead of `<body>`.
- Wrappers are cleaned before bundling: `<style>`, `<script>`, `<?php`, `?>`, `<html>`, `<body>`… so each source file may stay a valid file on its own.

### Change a shard while it is bundled

Give `shard()` a second callable. It receives the source and returns the new one:

```php
Crafter::shard('src/index.html', function($source) {
  return str_replace('Hello from Rune.', 'Built at ' . date('Y-m-d'), $source);
});
```

```html
<p id="hello">Built at 2026-10-23</p>
```

## What a spark does

`crafter_spark()` runs five steps, each with its own [arcane](arcane.md) line:

1. **clustering** — read every shard, run its injection, group by language.
2. **cleaning** — strip wrappers, minify what `MINIFIED` asks.
3. **bundling** — pick the template, bind the clusters with Weaver, add a hash from `cipher_id()` and the copyright line.
4. **distributing** — write `DIST` with Forger.
5. **message** — the `[√] Crafting … has been Sparked!!` lines, then Crafter resets to its default seed.

`Crafter::spark('page', fn)` runs `fn` between bundling and distributing.

## What you keep from this page

- item = what, seed = how, shard = from, spark = now.
- `TYPE` + `LANGUAGE` must match a template exactly.
- Next: [Bundling](bundling.md)
