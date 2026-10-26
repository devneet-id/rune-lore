# Exura

> A simple toolkit for the web, born after Crafter.

<!-- status: draft -->

Once you can bundle, you start to build websites — and a website wants a toolkit. Rune could have taken React or Tailwind, but each is a world of its own; bound into Rune they made things heavy instead of simple. So **Exura** was born: a small toolkit made to be bundled by Crafter, in the same spirit as the runes.

## What Exura is

Three files, one for each side of the web:

| Part | File | What it gives |
|---|---|---|
| **ExuraCSS** | `exura.css` | a base style (built on normalize.css), colour variables, and layout written as attributes: `flex="j:between"`, `size="w:full p:1"`, `text="bold"` |
| **ExuraJS** | `exura.js` | small reactive modules: `Exura.module()` with `state`, `effect`, `render`, `watch`, `router` |
| **ExuraPHP** | `exura.php` | a tiny router for APIs: `Exura::module('GET', 'route', fn)`, `Exura::state()`, `Exura::return()` |

They are plain files. Crafter bundles them like any other shard.

## How you get it

Exura comes as **shards of an Awakening template**. Start a new runite and choose a website template:

```
$ php cast
>>> Begin anew, or use an artefact [y/n]: y
[3] WEBSITE WITH EXURA(SD) TO VERCEL
 :: 2025-10-01 @Anwar Achilles [vercel, exuracss, exurajs, exuraphp]
[4] WEBSITE WITH EXURA(SD)
 :: 2025-10-01 @Anwar Achilles [exuracss, exurajs, exuraphp]
>>> Where would you like to continue your journey? [ID]: 4
[√] Awakening successfully.
```

You get a runite and a small site:

```
cast
src/
├── exura/
│   ├── exura.css
│   ├── exura.js
│   └── exura.php
├── index.head.html
├── index.html
├── index.css
├── index.js
└── index.php
dist/assets/background.jpg
README.md
.gitignore
```

## How it is bundled

The template's `build` cast is Crafter, exactly as you learned it:

```php
Chanter::cast(
  arg: 'build',
  echo: 'bundling to website applications',
  execute: function() {
    Crafter::item('my-rune-app', function() {
      Crafter::seed('DIST', __DIR__ . '/dist/index.php');
      Crafter::seed('TYPE', 'plain');
      Crafter::seed('LANGUAGE', ['html','css','js', 'php']);

      Forger::scan('src/exura/', function($item) {   // Exura first
        Crafter::shard($item->target);
      });

      Crafter::shard('src/index.head.html');          // then your page
      Crafter::shard('src/index.html');
      Crafter::shard('src/index.css');
      Crafter::shard('src/index.js');
      Crafter::shard('src/index.php');
    });
    Crafter::spark('my-rune-app');
  }
);
```

Exura and your page become one `dist/index.php`. The Vercel template splits it in two: `public/index.html` (`html`, `css`, `js`) and `api/index.php` (`php` only, with `exura.php`).

Your page then writes Exura:

```html
<div id="wrapper" flex="a:middle j:between d:column">
  <div size="w:full p:1" flex="j:between">
    <h4 text="bold">R U N E</h4>
  </div>
</div>
```

```php
// src/index.php
Exura::module('GET', 'demo', function() {
  Exura::state(200);
  return [
    'data' => 'Hello World 👋'
  ];
});
```

## The template's other casts

| Cast | Runes | Act |
|---|---|---|
| `build` | Crafter, Forger | this Act |
| `store` | `Keeper::shard()` — keeps assets for the artefact | this Act |
| `ready` | build + store, then `Forger::move()` into `ready/` | this Act |
| `watch`, `serve`, `start` | Specter (observe, dev server, another window) | [Act 3](../3-liberation-of-forte/README.md) |

You can run `build` now. The Specter casts wait for Act 3.

## Known issues

- On Linux and macOS, awakening the Exura templates writes the toolkit as files literally named `src/exura/\exura.css`, `\exura.js`, `\exura.php` (Windows paths inside the artefact). Rename them before you build, or the build runs without Exura:

  ```bash
  cd src/exura && for f in '\exura.css' '\exura.js' '\exura.php'; do mv -n "$f" "${f#\\}"; done
  ```

  After that, `php cast build` gives `dist/index.php` with 8 shards.
- `artefact --inspect` on these templates glitches (`Undefined array key "CAST"`); awakening them works.

## What you keep from this page

- Exura = ExuraCSS + ExuraJS + ExuraPHP, made to be bundled by Crafter.
- It comes as shards of the *Website with Exura* Awakening templates.
- Its `build` cast is plain Crafter.
- Next Act: [Liberation of Forte](../3-liberation-of-forte/README.md)
