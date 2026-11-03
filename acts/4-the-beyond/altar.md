# Altar

> The GUI to come — still 100% in development.

The Altar is where runites will be shaped by hand. Everything the CLI does — engraving, the Grimoire, relics — gets a window. It is the most powerful idea in Rune, and the least finished. **Treat it as a preview.**

## What exists
```bash
php cast sentinel --altar
```
Sentinel (`--altar`, hidden from its main hall) copies `@runite/sentinel/altar.txt` to `altar.php` in your working folder (once), then starts a server with Specter on **`127.0.0.1:8100`**. The runite needs Forger and Specter awake.

`altar.txt` is an old Crafter bundle (header `RUNE 1.0.10`), built with **Nirvana**, the web toolkit that is now Exura.

## Why it is not ready
- The UI is Nirvana; it must be rebuilt with **Exura** (planned).
- Its API runs a cast with `start cmd /k` — **Windows only** — and passes POST input **without sanitising** it. Run it only on your own machine.
- It still uses old paths: `.echoes/rune.php/` and a `shards/` folder.

## The plan
- **Edit runites** — the engraving, with the sentinel markers.
- **Help build the web** — Crafter and Exura in a window.
- **A readable Grimoire** — every Phantasm, node, link and arcane, easier than the terminal.
- **Make and inspect relics** — seal, inspect, open, shards.
- **Relics from the reliquaries** — browse `devneet-id/reliquary` and the federation in a window ([The Reliquary](reliquary.md)).
- **Report anomalies** — maintain runes through the GUI and report what it finds (the "Contribute with Altar" idea in `CONTRIBUTING.md`).

## How to help
Rebuilding Altar with Exura is planned. Start from [Exura](../2-understanding-its-flow/exura.md) and [Specter](../3-liberation-of-forte/specter.md); keep it local-only and sanitise every input.
