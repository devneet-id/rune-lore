# Versioning

> Every change raises a Phantasm; the footer counts them.

Rune counts its own growth. Each rune carries a version in its Phantasm; the footer of every run counts them. The count is the version of Rune — and the release tag.

## The footer
```
◇Version=1.20.110: ϟExecute=0.0070s, ΞMemory=975.42KB - ^1.14MB
```
`aether_version()` builds it, with **whole numbers** only:
1. Split `AETHER_VERSION` into major and minor (`'1.11'` → `1` and `11`).
2. Split every rune's `Phantasm::$version` into major and minor (`'1.18'` → `1` and `18`; `'0.10'` → `0` and `10`). A folder without a Phantasm is skipped.
3. `Version = <major> . <minor + sum of rune majors> . <sum of rune minors>`.

The ten origin runes today:

| | Aether | Chanter | Cipher | Crafter | Forger | Keeper | Minister | Specter | Weaver | Whisper | **Sum** |
|---|---|---|---|---|---|---|---|---|---|---|---|
| version | 1.18 | 1.14 | 1.6 | 1.13 | 1.14 | 1.13 | 0.3 | 1.9 | 1.7 | 1.13 | |
| major | 1 | 1 | 1 | 1 | 1 | 1 | 0 | 1 | 1 | 1 | **9** |
| minor | 18 | 14 | 6 | 13 | 14 | 13 | 3 | 9 | 7 | 13 | **110** |

→ `1 . (11 + 9) . 110` = `Version=1.20.110`.

The footer (`aether_version(true)`) also counts runes in `@liberations/` in liberation mode (not those named like an origin rune), so your footer can be higher than the official one — that is expected. Everything that must match between machines counts the **origin runes only** (`aether_version()`): the artefact header, `rune.json`, the copyright line of a Crafter bundle, and the release tag.

## Raise a version
Rule: **every change to a rune's Ether, Essence, Entity or Manifest raises that rune's Phantasm version.** `@bindrune/*` runites have no Phantasm and are not counted.

From a liberation runite (see [The Workshop](the-workshop.md)):
```bash
php liberate sentinel --phantasm-up=Weaver
```
`--phantasm-up` adds 1 to the minor: `1.7` → `1.8`, `1.9` → `1.10`. The footer's last number moves by one (`1.20.110` → `1.20.111`). Or edit `public $version` in `<Rune>/Phantasm.php` by hand — always `'<major>.<minor>'`, as a string.

`--phantasm-fix` raises the version only when it changed the Phantasm (node, link or note). A link records the version of the rune it leans on, so raising Aether changes the links of the runes that use it.

## Why it only goes up
- `--phantasm-up` on any rune → last number +1.
- A rune raises its major (`0.3` → `1.0`) → the middle number +1; the last may drop, and the version still goes up.
- A new origin rune → middle + its major, last + its minor.
- An origin rune removed → both drop: raise the minor of `AETHER_VERSION` enough to keep the version going up.
- Never lower a version by hand.

## Version, tag, package
- The footer `Version=` of a clean checkout (no `@liberations/`) is the **release tag**: `v1.20.110`.
- Packagist reads the tags. See [Release](release.md).
- The version also guards artefacts: an artefact made with a newer Rune is refused on revoke — *This artefact needs Rune X, you have Y.*
