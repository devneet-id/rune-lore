# Awakening

> From the silence of nothingness, echoes rise from the void.

Awakening turns an empty file into a runite. It asks one question — *begin anew, or use an artefact?* — then writes the chosen template into your file.

## In code
```php
#!/usr/bin/env php
<?php
require_once __DIR__ . '/vendor/autoload.php';

Rune\Ethereal::awakening();
```
```bash
php cast
```

## The flow
1. **A W A K E N I N G** — *Begin anew, or use an artefact [y/n]*
   - `n` → **Blank Starter** (the four runes of Act 0).
   - `y` → a list of artefacts from `@bindrune/awakening/src/`:
     | Template | Runes |
     |---|---|
     | Blank Starter | Aether, Whisper, Weaver, Chanter |
     | How to Casting | + casts, spells and notes examples |
     | Website with Exura (SD) | + Crafter, Exura |
     | Website with Exura (SD) to Vercel | + Crafter, Exura, Vercel |
2. The artefact is opened (runic → base64 → text): its **runite** replaces your file (starting with `#!/usr/bin/env php` when your file has no `.php`), its **shards** are written next to it.
3. *Awakening successfully. Checkout your runite with `php cast`.*

## Notes
- An artefact made with a newer Rune than yours is refused.
- After awakening, the file is no longer the awakening door — it is your runite. To awaken again, put the three lines above back.
- Template file names follow `Title.Date.Author.tags.rune` (URL-encoded).
- Templates will move to a registry of artefacts (`rune-artefacts`) so any `.rune` online can become a template.
