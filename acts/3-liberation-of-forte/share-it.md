# Share It

> Your app travels as an artefact — and can become a template.

<!-- status: draft -->

An app is finished when it can leave your folder. Seal it into one `.rune`, carry your own runes with it as shards, and bring it back to life anywhere Rune lives.

## 1 · Carry your rune as shards
A runite in liberation mode needs its runes. Add them to the shards with Keeper — with a path **relative to the runite's folder**:
```php
Chanter::cast('pack', function() {
  Keeper::shard(['@liberations/Ledger']);
  Whisper::echo("Ledger will travel with the artefact{{nl}}");
}, 'Add the Ledger rune to the shards.');
```
```
$ php cast pack
$ php cast artefact --shard-list
[1] 65c8277b08168476  php @liberations/Ledger/Entity.php
[2] dd474f6d0389acdf  php @liberations/Ledger/Essence.php
[3] cea3312f88a00f14  php @liberations/Ledger/Ether.php
[4] feca8f9849f2985f  php @liberations/Ledger/Manifest.php
[5] ea9054a5b8320c97  php @liberations/Ledger/Phantasm.php
```
**Trap:** `Keeper::shard([__DIR__ . '/@liberations/Ledger'])` stores **absolute** paths. On revoke the files are written back to that same absolute path — on another machine, a folder that does not exist. Run from the runite's folder and keep shard paths relative.

## 2 · Seal it
```bash
php cast artefact --invoke
```
```
[√]SUCCESS: Artefact successfully invoked.
```
`cast.rune` now holds the runite, its echoes (casts, runes) and the five Ledger files — base64, sealed with a runic variant.

## 3 · Bring it back somewhere else
In a new folder with Rune installed and a plain runite (the four runes are enough — Awakening's Blank Starter):
```bash
php cast artefact --inspect=../cast.rune    # read before you trust
php cast artefact --revoke=../cast.rune
php cast month
```
```
[√]SUCCESS: Artefact successfully revoked.
+ IDR 5,000,000  salary
- IDR 1,250,000  rent
- IDR 300,000  internet
= IDR 3,450,000
```
The runite replaced the plain one and `@liberations/Ledger/` was written next to it. The runite's own `require_once __DIR__ . '/…/vendor/autoload.php'` travels as written — revoke it at the same depth, or fix that line.

`--inspect` shows the casts (`month`, `pack`), the runes (including `Rune\Ledger\Manifest`) and the shards before anything is written. **An artefact is code: revoke only what you trust.**

## 4 · As a template
Every Awakening template is an artefact: `Blank Starter`, `How to Casting`, `Website with Exura`… live in Rune's `@bindrune/awakening/src/` as `Title.Date.Author.tags.rune` ([runites/awakening.md](../../runites/awakening.md)). Your `.rune` is the same kind of file.

**Planned:** templates will not be limited to the ones inside Rune. Each example app gets its own repo, and a registry — `rune-artefacts` — lists the links to their `.rune` files, so any artefact online can become a starting point ([The Artefact Registry](../4-the-beyond/artefact-registry.md)).

## What not to seal
- `familiar.json` and other tokens — shards are only obscured, not encrypted.
- `vendor/` — Rune comes from Composer on the other side.

Your runes, your apps, carried anywhere: that is the liberation of Forte. Next: [Act 4 · The Beyond](../4-the-beyond/README.md).
