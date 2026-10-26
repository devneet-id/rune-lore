# Resonance

> A runite can describe itself.

<!-- status: draft -->

Strike a runite and it resonates: it tells what it is — its name, its casts, the runes awake in it, its size and the memory it needs. Keeper keeps that answer as `rune.json`, and the artefact carries it when the runite travels.

## In code

Nothing to engrave. Every runite with Keeper can resonate:

```
$ php cast --resonance
```

Only a spell, no cast — so `Chanter::end()` runs the `rune` cast (the main screen) with `--resonance`. The main screen sees the spell and writes `.echoes/<runite>/rune.json`.

## `rune.json`

```json
{
  "FILE": "cast",
  "REPO": "_act2",
  "VERSION": "1.11",
  "CAST": {
    "artefact": ["artefact", "artefact", "To handle with shard & artefact."],
    "grimoire": ["grimoire", "grimoire", "will help you read the system structure and flow."],
    "rune": ["rune", "rune", "base of the rune"],
    "sentinel": ["sentinel", "sentinel", "Help you with maintain your runite as assistant."],
    "hello": ["hello", "hello --name", "Say hello."]
  },
  "SIZE": 2301,
  "MEMORY": [1158536, 1339152],
  "RUNE": {
    "0": "Rune\\Whisper\\Manifest",
    "1": "Rune\\Weaver\\Manifest",
    "2": "Rune\\Chanter\\Manifest",
    "3": "Rune\\Forger\\Manifest",
    "4": "Rune\\Cipher\\Manifest",
    "5": "Rune\\Keeper\\Manifest",
    "8": "Rune\\Aether\\Manifest"
  }
}
```

| Key | What |
|---|---|
| `FILE` | the runite (`AETHER_FILE`) |
| `REPO` | the folder name it was run from |
| `VERSION` | `AETHER_VERSION` — Aether's own version line, **not** the footer `Version=` |
| `CAST` | every cast: `[name, signature with spells, echo]` |
| `SIZE` | the runite file, in bytes |
| `MEMORY` | memory used and peak, in bytes |
| `RUNE` | the awakened runes (`aether_arised()`) |

## Who reads it

- **The main screen.** `php cast` lists what the echoes hold: `Echoes » Rune, Arcane, Glitch, Shards,` — *Rune* means `rune.json` is there.
- **The artefact.** `artefact --invoke` puts it in the `ECHOES` block of the `.rune` file. Never resonated? The artefact builds it itself, so nothing is lost. See [Artefact](../../runites/artefact.md).

## When to resonate

- Before `artefact --invoke`, so the artefact carries today's casts.
- After you add or rename casts, to see the runite as others will see it.
- To compare size and memory between two versions of your runite.

## What you keep from this page

- `php cast --resonance` writes `.echoes/<runite>/rune.json`.
- It holds the runite's casts, runes, size and memory.
- The artefact carries it.
- Next: [Crafter](crafter.md)
