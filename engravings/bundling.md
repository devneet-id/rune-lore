# Bundle a Small Website

> Bundle HTML, CSS, JS and PHP from `src/` into one file.

**Runes:** Crafter, Forger, Weaver · **From:** Act 2

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

## How it works
- `seed` is the recipe: output file, type (`plain`, `class`, `function`), languages.
- Every `shard` is a source file; a file named `*.head.html` goes into `<head>`.
- `spark` cleans, minifies (when asked), bundles and writes the result.
