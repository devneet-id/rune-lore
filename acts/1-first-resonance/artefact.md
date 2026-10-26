# Artefact

> An artefact is a runite preserved to travel: its code, its echoes, its shards — sealed into one `.rune` file and brought back to life anywhere.

→ Reference: [artefact](../../runites/artefact.md)

In [Act 0](../0-the-void/reading-the-grimoire.md) you met the Grimoire — the book that reads a rune. The Artefact is its twin: it reads your **runite**, seals it, and opens it again.

You have already used one: the Blank Starter that [Awakening](../../runites/awakening.md) wrote for you came out of an artefact.

## Shards: what travels with the app
The runite alone is not the whole app — `weaver/row.txt` is part of it. Tell Keeper which files travel, right after `Keeper::begin()`:

```php
// the row template travels with the artefact
Keeper::shard(['weaver', 'export']);
```

```bash
php cast artefact --shard-list
```
```
[NO] [ID] [EXTENSION] [TARGET]
[1] d494ffa600b70f02  txt weaver/row.txt
[2] 9166f8e18ac147b8  txt export/notes.txt
```

- A folder adds every file inside it. Paths are relative to the runite's folder.
- `.echoes` never becomes a shard.
- `--shard-remove=<id>` drops one, `--shard-clean` drops all.
- While Keeper is awake, files Forger reads or writes **by a path relative to the runite** are added on their own (`FORGER_KEEPER_SHARD`). Check the list before you seal.

## Seal: `--invoke`
```bash
php cast artefact --invoke
```
```
[√]SUCCESS: Artefact successfully invoked.
```

`cast.rune` appears next to the runite:

```
The Artefact of Runite

[ᚱᚾ] A R T E F A C T
  ::time=1792760128
  ::version=1.11
  ::runic=anglo_saxon_futhorc
  ::encryption=base64
  ::php=8.3.6
  …
[ᚱᚾ] R U N I T E
  ::IᛃEvᛞXNᛃL2Jᛈᛒᛁ9ᛚᛒᚾYᚷᚲGᚺ…
[ᚱᚾ] E C H O E S
[ᚱᚾ] S H A R D S
```

Base64, then sealed with the [runic cipher](cipher.md#secrets). Four blocks: the artefact's facts, the runite, its echoes (what the runite says of itself), its shards.

## Look before you trust: `--inspect`
An artefact *is* code. Read it before you open it:

```bash
php cast artefact --inspect=cast.rune
```
```
 ♦ Rune & PHP Version
    » 1.11 with PHP 8.3.6
    You » 1.11 with PHP 8.3.6

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

## Bring it back: `--revoke`
In a new folder with any runite — the Blank Starter is enough:

```bash
php cast artefact --revoke=../notes/cast.rune
```
```
[√]SUCCESS: Artefact successfully revoked.
```

- The artefact's runite **replaces** this runite.
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

## Traps
- Revoke only what you trust, and inspect first.
- Known issue: an artefact with **exactly one** shard breaks. `--inspect` glitches, and `--revoke` says *success* but does not write the shard. Carry none, or two and more.
- Without Keeper an artefact carries the runite only.

## The end of the Act
You resonated with seven runes and built one app with them. It speaks, asks, remembers, writes files, and travels as one sealed file.

Next: [Act 2 · Understanding Its Flow](../2-understanding-its-flow/README.md).
