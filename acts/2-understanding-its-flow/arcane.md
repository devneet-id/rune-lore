# Arcane

> Every step leaves a trace.

<!-- status: draft · sources: Aether/Entity.php (aether_arcane), Keeper/Entity.php (keeper_arcane_process), Keeper/Essence.php ($KEEPER_ARCANE), @bindrune/chanter/grimoire/cast.php -->

While the flow runs, every rune whispers what it does to Aether: *Chanter cast*, *Forger item*, *Weaver bind*. That trace is the **arcane**. Keeper writes it down when the flow ends, so you can read how your runite really moved.

## Where it is

| File | What |
|---|---|
| `.echoes/<runite>/arcane.txt` | the arcane of the **last** run |
| `.echoes/<runite>/arcanes/<date>.txt` | one copy per run, e.g. `2026-10-23--12-52-27.txt` |

Keeper must be engraved (`Keeper::begin()` … `Keeper::end()`). Without it the arcane lives in memory and is lost at `exit`.

## One line

```
[2026-10-23 12:52:27] - [0.0023] - [0.00227] - Aether.manifest.begin: -  - //FLOW
```

| Part | Meaning |
|---|---|
| `[2026-10-23 12:52:27]` | when |
| `[0.0023]` | **stopwatch** — seconds since `Aether::begin()` |
| `[0.00227]` | **stepwatch** — seconds since the line before |
| `Aether.manifest.begin` | who: `Rune.part.name` — a Manifest call or an Entity function |
| `//FLOW` | the **state** of this step |

## States

The state comes from the stepwatch — how long this one step took.

| State | From | |
|---|---|---|
| BURST | 0 s | instant |
| FLASH | 0.0001 s | |
| FLOW | 0.001 s | normal work (loading, the first file write) |
| FALL | 2 s | slow |
| BREAK | 5.5 s | |
| COLLAPSE | 8.5 s | |
| OVERCLOCK | 10 s | something waits too long |

The thresholds live in `$KEEPER_ARCANE` (Keeper's Essence).

## Read it with the Grimoire

```
$ php cast hello --name=Anwar
$ php cast grimoire --arcane
 0 | λ2026-10-23 12:52:31 ϟ0.0022s ϟ0.00223s   .::FLOW::.   [ϻ] Aether.manifest.begin:
 1 | λ2026-10-23 12:52:31 ϟ0.0026s ϟ0.00041s   .::FLASH::.   [ͱ] Chanter.entity.chanter_arg_extract:
 2 | λ2026-10-23 12:52:31 ϟ0.0026s ϟ0.00000s   .::BURST::.   [ͱ] Chanter.entity.chanter_set:
 ...
CURRENT ARCANE STATS:
[i]labels states up to: 0s=BURST, 0.0001s=FLASH, 0.001s=FLOW, 2s=FALL, 5.5s=BREAK, 8.5s=COLLAPSE, 10s=OVERCLOCK,
  Execute » 	Process = 41, End in = 0.0044s
  Module » 	Manifest = 6, Entity = 14
  Stepwatch » 	Average = 0.00011s, Up to = 0.00227s
  State » 	FLOW = 1, FLASH = 5, BURST = 34,
```

| Symbol | Meaning |
|---|---|
| `λ` | time |
| `ϟ` | stopwatch, then stepwatch |
| `[ϻ]` | a Manifest call |
| `[ͱ]` | an Entity call |

`grimoire --arcane` shows `arcane.txt` — the run **before** it. `grimoire --arcane-clean` empties `arcanes/`.

## What the arcane tells you

Read the `hello` run from the top and you see [the flow](the-flow.md) itself:

1. `Aether.manifest.begin` — the flow opens.
2. Four `chanter_arg_extract → chanter_set → chanter_echo_set → Chanter.manifest.cast` groups — the four built-in casts from `Chanter::begin()`.
3. `forger_fix`, `forger_item` — `Keeper::begin()` making `.echoes`.
4. One more group — your `hello` cast, registered.
5. `chanter_spell_chain`, `chanter_get`, `chanter_spell_get` — `Chanter::end()` finding and running `hello`.
6. `Weaver… bind`, `Whisper… echo` — the cast's own work.
7. `Chanter.manifest.awaken`, `Keeper.manifest.end` — the flow closes.

`Aether.manifest.end` is never in the file: Keeper writes before Aether ends.

## Quiet details

- The same name twice in a row is written once: a line is skipped when it equals one of the two before it.
- `--zero-trust` turns the arcane off (see [Cast in Cast](cast-in-cast.md#zero-trust)).
- When the flow breaks, `Keeper::end()` is never reached: `arcane.txt` still holds the run before. Read the [Glitch](glitch.md) instead.

## Leave your own trace

`aether_arcane()` is an Entity function — you can call it too:

```php
aether_arcane('Notes.cast.import', 'rows=120');
```

```
[2026-10-23 12:55:38] - [0.0066] - [0.00000] - Notes.cast.import: - rows=120 - //BURST
```

## What you keep from this page

- `arcane.txt` = the last run, step by step, with time and state.
- `grimoire --arcane` reads it; Keeper must be engraved.
- Next: [Glitch](glitch.md)
