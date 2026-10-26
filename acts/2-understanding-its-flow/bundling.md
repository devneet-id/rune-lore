# Bundling

> Many source files become one distributable file.

<!-- status: draft -->

You write in many small files — one for the look, one for the logic, one for the words. The world wants one file it can open, require or upload. Bundling is how a runite carries the many into the one.

## A page: HTML + CSS + JS

```
site/
├── cast
└── src/
    ├── index.head.html   <title>Ember</title>
    ├── index.html        <h1>Ember</h1> <p id="hello">Hello from Rune.</p>
    ├── index.css         <style> body {…} h1 {…} </style>
    └── index.js          document.getElementById('hello').textContent += ' (bundled)';
```

```php
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

`dist/index.html`:

```html
<!DOCTYPE html>
<html>
<!-- RUNE 1.11 | Created By @anwarachilles -->
<head>
<title>Ember</title>
  <style>
body{font-family:sans-serif}h1{color:#c0392b}
  </style>
</head>
<body>
  <h1>Ember</h1>
<p id="hello">Hello from Rune.</p>
  <script>
document.getElementById('hello').textContent+=' (bundled)';
  </script>
</body>
</html>
```

The `<style>` tags of `index.css` were cleaned away; CSS and JS were minified.

## Many shards at once

List a folder with Forger and add each file:

```php
Crafter::item('all', function() {
  Crafter::seed('DIST', AETHER_REPO . '/dist/all.html');
  Crafter::seed('TYPE', 'plain');
  Crafter::seed('LANGUAGE', ['html', 'css', 'js']);
  Forger::scan('src', function($item) {
    Crafter::shard($item->target);
  });
});
```

A shard whose language is not in `LANGUAGE` is counted but left out of the result.

## A PHP page: plain, function, class

Add PHP and the result is a `.php` page. `app/page.php` holds the logic, `app/page.html` uses it:

```php
// app/page.php
<?php
function hello( $name ) {
  return "Hello, $name.";
}
```

```html
<!-- app/page.html -->
<h1><?= hello('Rune') ?></h1>
```

```php
Chanter::cast('build-app --type', function() {
  $type = Chanter::spell('type');
  $type = ($type && $type !== '1') ? $type : 'plain';
  Crafter::item('app', function() use ($type) {
    Crafter::seed('DIST', AETHER_REPO . "/dist/app.$type.php");
    Crafter::seed('TYPE', $type);
    Crafter::seed('LANGUAGE', ['html', 'css', 'js', 'php']);
    Crafter::shard('app/page.html');
    Crafter::shard('app/page.css');
    Crafter::shard('app/page.js');
    Crafter::shard('app/page.php');
  });
  Crafter::spark('app');
}, 'Bundle app/ into one PHP page. --type=plain|function|class');
```

```
$ php cast build-app --type=plain
[i]INFO: Path=/.../dist/app.plain.php, Size=307.00B, Shard=4
$ php cast build-app --type=function
[i]INFO: Path=/.../dist/app.function.php, Size=1.97KB, Shard=4
$ php cast build-app --type=class
[i]INFO: Path=/.../dist/app.class.php, Size=1.98KB, Shard=4
```

All three give the same page when run:

```
$ php dist/app.class.php
<!DOCTYPE html>
...
  <h1>Hello, Rune.</h1>
...
```

| `TYPE` | The file | Choose it when |
|---|---|---|
| `plain` | readable: PHP on top, the page below | you want to read and edit the result |
| `function` | every part kept as base64 inside functions, rebuilt and run with `eval` | you want one file whose source is not plain to the eye |
| `class` | the same, inside a class named after a hash (`RUNE_<hash>`) | you prefer its helpers as methods of one class instead of global `rune__*` functions |

Base64 hides, it does not protect. Anyone can decode it.

## Only PHP, or only CSS

`TYPE` `plain` with one language gives one clean file:

```php
Crafter::seed('DIST', AETHER_REPO . '/dist/hello.plain.php');
Crafter::seed('TYPE', 'plain');
Crafter::seed('LANGUAGE', ['php']);
Crafter::shard('src/hello.php');
```

```php
<?php
/* RUNE 1.11 | Created By @anwarachilles */
function hello( $name ) {
  return "Hello, $name.";
}
```

Then use it like any PHP file:

```php
Chanter::cast('use', function() {
  require AETHER_REPO . '/dist/hello.plain.php';
  Whisper::echo(hello('Rune') . '{{nl}}');
}, 'Use the bundled PHP.');
```

```
$ php cast use
Hello, Rune.
```

`function` and `class` always build a whole page — they are for apps, not for libraries.

## Ship it

The bundle is a plain file. Open the `.html` in a browser, serve the `.php` with any PHP server (`php -S localhost:8000 -t dist`), upload it, or put it in a release. To carry the runite that builds it, seal it as an [artefact](../../runites/artefact.md).

## What you keep from this page

- `plain` + `['html','css','js']` → an `.html` page; add `php` → a `.php` page.
- `function` / `class` hide the source in base64; the page is the same.
- `Forger::scan()` adds a whole folder of shards.
- More recipes: [engravings/bundling.md](../../engravings/bundling.md)
- Next: [Exura](exura.md)
