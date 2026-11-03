# Share It

> Your app travels as a relic — and can live in a reliquary.

An app is finished when it can leave your folder. Seal it into one relic (`.rune`), carry your own runes with it as shards, and bring it back to life anywhere Rune lives.

## 1 · Carry your rune as shards
A runite in liberation mode needs its runes. Add them to the shards with Keeper — with a path **relative to the runite's folder**:
```php
Chanter::cast('pack', function() {
  Keeper::shard(['@liberation/Ledger']);
  Whisper::echo("Ledger will travel with the relic{{nl}}");
}, 'Add the Ledger rune to the shards.');
```
```
$ php cast pack
$ php cast reliquary --shards
[1] 65c8277b08168476  php @liberation/Ledger/Entity.php
[2] dd474f6d0389acdf  php @liberation/Ledger/Essence.php
[3] cea3312f88a00f14  php @liberation/Ledger/Ether.php
[4] feca8f9849f2985f  php @liberation/Ledger/Manifest.php
[5] ea9054a5b8320c97  php @liberation/Ledger/Phantasm.php
```
Shard paths are kept **relative to the runite's folder** — even `Keeper::shard([__DIR__ . '/@liberation/Ledger'])` is stored as `@liberation/Ledger/…` — so when the relic is opened the files land next to the new runite. Files outside the runite's folder are not carried.

## 2 · Seal it
```bash
php cast reliquary --runite-relic
```
```
[√]SUCCESS: Relic made: cast.rune
```
`cast.rune` now holds the runite, its echoes (casts, runes) and the five Ledger files — base64, sealed with a runic variant.

## 3 · Bring it back somewhere else
In a new folder with Rune installed and a plain runite (the blank one of Awakening is enough):
```bash
php cast reliquary --runite-inspect=../cast.rune        # read before you trust
php cast reliquary --relic-runite=../cast.rune --yes
php cast month
```
```
[√]SUCCESS: ../cast.rune opened into cast
+ IDR 5,000,000  salary
- IDR 1,250,000  rent
- IDR 300,000  internet
= IDR 3,450,000
```
The runite replaced the plain one and `@liberation/Ledger/` was written next to it. The runite's own `require_once __DIR__ . '/…/vendor/autoload.php'` and its `Rune\Ethereal::liberation();` travel as written — open it at the same depth, or fix the `require` line.

`--runite-inspect` shows the casts (`month`, `pack`), the runes (including `Rune\Ledger\Manifest`) and the shards before anything is written. **A relic is code: open only what you trust.**

## 4 · Into a reliquary
A relic on your disk reaches one folder. A relic in a **reliquary** reaches everyone:

1. Put the app in its own repo (e.g. `<you>/wallet`) with its `cast.rune`, and tag a version.
2. List it in a reliquary — your fork of [`devneet-id/reliquary`](https://github.com/devneet-id/reliquary) — in `relic.json`, with the link to the `.rune` and its `sha256`.
3. Anyone can then open it:
   ```bash
   php cast reliquary --relic-runite=<you>/wallet
   ```
   and, with Awakening, begin a new runite from it.

How reliquaries connect — forks of forks — is [The Reliquary](../4-the-beyond/reliquary.md) in Act 4.

## What not to seal
- `familiar.json` and other tokens — shards are only obscured, not encrypted.
- `vendor/` — Rune comes from Composer on the other side.

Your runes, your apps, carried anywhere: that is the liberation of Forte. Next: [Act 4 · The Beyond](../4-the-beyond/README.md).
