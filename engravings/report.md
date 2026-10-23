# HTML Report from Templates

> Weave templates into an HTML file, minify it, write it.

**Runes:** Weaver, Forger · **From:** Act 1

```php
// weaver/row.html:    <li>{{text}}</li>
// weaver/report.html: <html><body><h1>{{title}}</h1><ul>{{rows}}</ul></body></html>
Chanter::cast('report --min', function() {
  $rows = '';
  foreach (['Write docs', 'Ship release'] as $text) {
    // false: these values belong to one row, don't keep them in the bond
    $rows .= weaver_bind_multiple(Weaver::item(__DIR__ . '/weaver/row.html'), ['text' => $text], false);
  }
  $html = Weaver::bind(Weaver::item(__DIR__ . '/weaver/report.html'), ['title' => 'Todo', 'rows' => $rows]);
  if (Chanter::spell('min')) {
    $html = weaver_min($html, 'html');
  }
  Forger::fix(Forger::trace(AETHER_REPO . '/dist/report.html'));
  Forger::item(AETHER_REPO . '/dist/report.html', $html);
  Whisper::echo('dist/report.html written{{nl}}');
}, 'Write an HTML report from templates. --min');
```

## How it works
- `Weaver::item($file)` loads a template once and keeps it in memory.
- `weaver_bind_multiple($template, $data, false)` binds without remembering the values in the bond — right for repeated rows.
- `weaver_min($html, 'html')` removes comments and spaces (`css`, `js`, `php` too).

**Full, tested example:** `rune-dev/scenario/05-todo`
