# Keeper

> Keeper is the memory of a runite. With it, the app remembers — and `.echoes` appears for the first time.

<!-- status: draft · sources: runes/keeper.md, scenario/02-notes, 06-multicast, 07-nested -->

→ Reference: [Keeper](../../runes/keeper.md)

## Remember the notes
Replace the empty array with what Keeper holds, and keep the notes after every change:

```php
// the notes live in .echoes/<runite>/notes.json
$NOTES = (array) (Keeper::item('notes') ?: []);
function notes_keep() {
  global $NOTES;
  return Keeper::item('notes', (object) $NOTES);
}
```

Then call `notes_keep();` after each add, edit and remove.

- `Keeper::item('notes')` reads. It gives an **object** (or `null` when there is nothing yet) — `(array)` turns it back.
- `Keeper::item('notes', $data)` writes `notes.json`.
- Write `(object) $NOTES` so `notes.json` is always a JSON object, whatever the keys — even when the list is empty (`{}`). (`Keeper::item()` reads only when the second argument is left out; the Entity `keeper_item()` treats any empty value as a read.)

Make sure `Keeper::begin()` / `Keeper::end()` are in place ([Sentinel](sentinel.md#the-trap-keeper-needs-begin-and-end)).

## It remembers
```bash
php cast note --add="Buy milk"
php cast note --add="Call mom"
php cast notes
```
```
[√] Added #1
[√] Added #2
#1 Buy milk
#2 Call mom
```

Three runs, one memory.

## `.echoes` appears
```
notes/
├── cast
├── weaver/
└── .echoes/
    └── cast/                 one folder per runite
        ├── notes.json        your item
        ├── arcane.txt        the trace of the last run
        ├── arcanes/          the trace of every run, by date
        ├── glitch.txt        the last error, if any
        └── shard.json        files that travel with the artefact
```

```json
{
  "0": "Buy oat milk"
}
```

Now the Grimoire can read the flow:

```bash
php cast grimoire --arcane
```
```
 103 | λ2026-10-23 12:55:45 ϟ0.0087s ϟ0.00000s   .::BURST::.   [ϻ] Keeper.manifest.end:

CURRENT ARCANE STATS:
  Execute »   Process = 105, End in = 0.0087s
  Module »    Manifest = 13, Entity = 21
```

Reading the arcane is [Act 2](../2-understanding-its-flow/arcane.md). For now: every step of the run is there.

## Run it from its own folder
`.echoes` is made in the folder you run from, not the folder of the runite (T48, to be fixed). From the parent folder:

```bash
cd ..
php notes/cast notes
```
```
No notes yet.
```

…and a second `.echoes/notes/cast/` appears in the parent. Always `cd` into the runite's folder first.

## Trap
Known issue: writing with `Keeper::echo()` glitches. Use `Keeper::item()` for data, and [Forger](forger.md) for plain files.

Next: [Forger](forger.md).
