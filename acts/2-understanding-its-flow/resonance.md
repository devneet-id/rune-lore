# Resonance

> A runite can describe itself.

Strike a runite and it resonates: it tells what it is — its name, its casts, the runes awake in it, its size and the memory it needs. Keeper keeps that answer as `rune.json`, and the relic carries it when the runite travels.

## In code

Nothing to engrave. Every runite with Keeper can resonate:

```
$ php cast --resonance
```

Only a spell, no cast — so `Chanter::end()` runs the `rune` cast (the main hall) with `--resonance`. The main hall sees the spell and writes `.echoes/<runite>/rune.json`.

## `rune.json`

```json
{
  "FILE": "cast",
  "REPO": "_act2",
  "VERSION": "1.20.114",
  "CAST": {
    "grimoire": ["grimoire", "grimoire", "Read the runes and the arcane of this runite."],
    "reliquary": ["reliquary", "reliquary", "Make, open and share relics (runite ⇄ .rune)."],
    "rune": ["rune", "rune", "The main hall of the runite."],
    "sentinel": ["sentinel", "sentinel", "Help you maintain your runite as an assistant."],
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
| `REPO` | the name of the runite's folder |
| `VERSION` | the version of Rune from the origin runes (`aether_version()`) — the release version |
| `CAST` | every cast: `[name, signature with spells, echo]` |
| `SIZE` | the runite file, in bytes |
| `MEMORY` | memory used and peak, in bytes |
| `RUNE` | the awakened runes (`aether_arised()`) |

## Who reads it

- **The main hall.** `php cast` lists what the echoes hold: `Echoes » Rune, Arcane, Glitch, Shards,` — *Rune* means `rune.json` is there.
- **The relic.** `reliquary --runite-relic` puts it in the `ECHOES` block of the `.rune` file. Never resonated? The relic builds it itself, so nothing is lost. See [Reliquary](../../runites/reliquary.md).

## When to resonate

- Before `reliquary --runite-relic`, so the relic carries today's casts.
- After you add or rename casts, to see the runite as others will see it.
- To compare size and memory between two versions of your runite.

## What you keep from this page

- `php cast --resonance` writes `.echoes/<runite>/rune.json`.
- It holds the runite's casts, runes, size and memory.
- The relic carries it.
- Next: [Crafter](crafter.md)
