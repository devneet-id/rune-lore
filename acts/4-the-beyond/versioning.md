# Versioning

> Every change raises a Phantasm; the footer adds them up.

<!-- status: draft -->

Rune counts its own growth. Each rune carries a version in its Phantasm; the footer of every run sums them. The sum is the version of Rune — and the release tag.

## The footer
```
◇Version=1.12.31: ϟExecute=0.0070s, ΞMemory=975.42KB - ^1.14MB
```
`aether_exit()` builds `Version=`:
1. Take the major of `AETHER_VERSION` (`'1.11'` → `1`).
2. For every rune in `aether_list_runes()`, add `(float) Phantasm::$version`. A folder without a Phantasm is skipped.
3. Print `major . '.' . sum`.

The ten origin runes today:

| Aether | Chanter | Cipher | Crafter | Forger | Keeper | Minister | Specter | Weaver | Whisper | **Sum** |
|---|---|---|---|---|---|---|---|---|---|---|
| 1.17 | 1.13 | 1.6 | 1.12 | 1.14 | 1.12 | 0.3 | 1.9 | 1.7 | 1.13 | **12.31** |

→ `Version=1.12.31`.

In liberation mode, runes in `@liberations/` are counted too (not those named like an origin rune). Your footer can differ from the official one — that is expected.

## Raise a version
Rule: **every change to a rune's Ether, Essence, Entity or Manifest raises that rune's Phantasm version.** `@bindrune/*` runites have no Phantasm and are not counted.

From a liberation runite (see [The Workshop](the-workshop.md)):
```bash
php liberate sentinel --phantasm-up=Weaver
```
`--phantasm-up` adds 1 to the part after the dot and keeps its width: `1.7` → `1.8`. The footer moves by `0.1` (`1.12.31` → `1.12.41`). Or edit `public $version` in `<Rune>/Phantasm.php` by hand.

## The float trap
Versions are summed as **floats**. `1.10` is `1.1`, smaller than `1.9`. So `--phantasm-up` on `1.9` writes `1.10` and the footer **goes down**. Until this is decided, never cross `x.9 → x.10`; plan the bump by hand. *(Open decision.)*

## Version, tag, package
- The footer `Version=` of a clean checkout is the **release tag**: `v1.12.31`.
- Packagist reads the tags. See [Release](release.md).
- `AETHER_VERSION` (`1.11`) also guards artefacts: an artefact made with a newer version is refused on revoke.
