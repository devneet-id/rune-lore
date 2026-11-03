# Relic

> A relic is a runite preserved to travel: its code, its echoes, its shards — sealed into one `.rune` file and brought back to life anywhere.

→ Reference: [reliquary](../../runites/reliquary.md)

In [Act 0](../0-the-void/reading-the-grimoire.md) you met the Grimoire — the book that reads a rune. The Reliquary is its twin: it reads your **runite**, seals it into a relic, and opens it again.

You may have used one already: [Awakening](../../runites/awakening.md) can begin your runite from a relic of `devneet-id/reliquary`.

## Shards: what travels with the app
The runite alone is not the whole app — `weaver/row.txt` is part of it. Tell Keeper which files travel, right after `Keeper::begin()`:

```php
// the row template travels with the relic
Keeper::shard(['weaver', 'export']);
```

```bash
php cast reliquary --shards
```
```
[NO] [ID] [EXTENSION] [TARGET]
[1] d494ffa600b70f02  txt weaver/row.txt
[2] 9166f8e18ac147b8  txt export/notes.txt
```

- A folder adds every file inside it. Paths are relative to the runite's folder. A file without extension travels too.
- `.echoes` never becomes a shard.
- `--shard=<id>` inspects one, `--shard-remove=<id>` drops one, `--shard-clean` drops all.
- While Keeper is awake, files Forger reads or writes **inside the runite's folder** are added on their own (`FORGER_KEEPER_SHARD`). Files outside it are never carried. Check the list before you seal.

## Seal: `--runite-relic`
```bash
php cast reliquary --runite-relic
```
```
[√]SUCCESS: Relic made: cast.rune
```

`cast.rune` appears next to the runite:

```
The Relic of Runite

[ᚱᚾ] R E L I C
  ::time=1793300128
  ::version=1.20.114
  ::runic=anglo_saxon_futhorc
  ::encryption=base64
  ::php=8.3.6
  …
[ᚱᚾ] R U N I T E
  ::IᛃEvᛞXNᛃL2Jᛈᛒᛁ9ᛚᛒᚾYᚷᚲGᚺ…
[ᚱᚾ] E C H O E S
[ᚱᚾ] S H A R D S
```

Base64, then sealed with the [runic cipher](cipher.md#secrets). Four blocks: the relic's facts, the runite, its echoes (what the runite says of itself), its shards.

## Look before you trust: `--runite-inspect`
A relic *is* code. Read it before you open it:

```bash
php cast reliquary --runite-inspect=cast.rune
```
```
 ♦ Rune & PHP Version
    » 1.20.114 with PHP 8.3.6
    You » 1.20.114 with PHP 8.3.6

 #  C A S T
 ♦ note --add --edit --remove --text
   ≈ Add, edit or remove a note. --add="text" --edit=<id> --text="text" --remove=<id>
 ♦ notes
   ≈ List the notes.
 ♦ export
   ≈ Write the notes to export/notes.txt.
 ♦ import --file
   ≈ Add every line of a text file as a note. --file=notes.txt

 #  R U N E
 ♦ Rune\Whisper\Manifest
 …
 #  S H A R D
 ♦ txt 59.00B weaver/row.txt
 ♦ txt 22.00B export/notes.txt
```

Its casts, its runes, its shards — and whether your Rune and PHP match the ones it was made with.

## Bring it back: `--relic-runite`
In a new folder with any runite — the blank one is enough:

```bash
php cast reliquary --relic-runite=../notes/cast.rune
```
```
[!] cast will be replaced by ../notes/cast.rune (+ 2 shard).
>>> Continue? [y/n]: y
[√]SUCCESS: ../notes/cast.rune opened into cast
```

- The relic's runite **replaces** this runite (`--yes` skips the question).
- Its shards are written next to it: `weaver/row.txt`, `export/notes.txt`.

```bash
php cast notes
php cast import
php cast notes
```
```
No notes yet.
[√] Added n6adb5959d77e2
[√] Added n6adb5959d786e
#n6adb5959d77e2 Buy oat milk
#n6adb5959d786e Call mom
2 notes
```

The app came back. Its **memory** did not — `notes.json` lives in `.echoes`, and items do not travel. The exported file did, so `import` brings the notes home.

## From the reliquary
A relic does not have to be on your disk. [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary) keeps relics online, like packages:

```bash
php cast reliquary --relics
php cast reliquary --relic=devneet-id/how-to-casting
php cast reliquary --relic-runite=devneet-id/how-to-casting
```

The newest version is downloaded, checked against its seal (sha256) and opened. Your own reliquary comes later, in [Act 4](../4-the-beyond/reliquary.md). More in the [reference](../../runites/reliquary.md#online-the-reliquary).

## Traps
- Open only what you trust, and inspect first — online relics most of all.
- Without Keeper a relic carries the runite only.
- A relic made with a newer Rune than yours is refused.

## The end of the Act
You resonated with seven runes and built one app with them. It speaks, asks, remembers, writes files, and travels as one relic.

Next: [Act 2 · Understanding Its Flow](../2-understanding-its-flow/README.md).
