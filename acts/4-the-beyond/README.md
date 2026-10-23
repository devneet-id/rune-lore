# Act 4 · The Beyond

> Past the last rune. You see Rune from the inside — and you can keep it alive without asking its first creator.

**Runes in this Act:** all of them — origin and your own
**You learn:** how Rune is built inside, the laws it keeps, how to test, version and release it, how to contribute — and where it goes next.

Until now you used Rune. From here you **keep** it. Every page in this Act points at real files in the `rune` repo and the `rune-dev` workshop, so you can check each claim yourself.

## I · Inside Rune
1. [Anatomy](anatomy.md) — the package from the inside
2. [Laws](laws.md) — the rules Rune keeps
3. [Decisions](decisions.md) — why things are the way they are

## II · Keeping Rune
4. [The Workshop](the-workshop.md) — `rune-dev`: live, scenario, trials, coverage
5. [Versioning](versioning.md) — Phantasm versions, the footer, the tag
6. [Release](release.md) — commit, tag, GitHub, Packagist
7. [Known Issues](known-issues.md) — what is still open

## III · Contributing
8. [Contributing](contributing.md) — from an issue to a merged change
9. [Keeping the Lore](keeping-the-lore.md) — updating `rune-lore` with the code

## IV · Beyond
10. [Every Repo Is a Runite](every-repo-is-a-runite.md) — Rune manages Rune; any repo can too
11. [The Artefact Registry](artefact-registry.md) — templates from anywhere
12. [Altar](altar.md) — the GUI to come
13. [The Road Ahead](the-road-ahead.md) — where Rune is heading

## The cycle you will repeat
```
find (issue, trial, known issue)
  → prove it   (a trial in rune-dev/scenario)
  → change it  (Entity first, Manifest only forwards, #NOTE above every node)
  → contract   (sentinel --phantasm-fix / --phantasm-up)
  → test       (php cast test, php cast trials)
  → commit     (type(scope): summary)
  → release    (tag = footer Version=)
  → lore       (rune-lore follows the code)
```
