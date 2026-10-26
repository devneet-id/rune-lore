# Sentinel

> The Sentinel guards the runite. Ask it, and it brings a rune in — or takes it out.

<!-- status: draft -->

→ Reference: [sentinel](../../runites/sentinel.md)

## Invoke three runes
```bash
php cast sentinel --invoke=Forger
php cast sentinel --invoke=Cipher
php cast sentinel --invoke=Keeper
```
```
[√] Successfully do Invoked with 'Keeper'
```

## What changed in the file
Sentinel writes at the two markers:

```diff
 use Rune\Chanter\Manifest as Chanter;
+use Rune\Forger\Manifest as Forger;
+use Rune\Cipher\Manifest as Cipher;
+use Rune\Keeper\Manifest as Keeper;
 #sentinel-manifest
 Aether::ether()::essence()::entity();
 Whisper::ether()::essence()::entity();
 Weaver::ether()::essence()::entity();
 Chanter::ether()::essence()::entity();
+Forger::ether()::essence()::entity();
+Cipher::ether()::essence()::entity();
+Keeper::ether()::essence()::entity();
 #sentinel-awaken
```

That is all: the [Manifest](../0-the-void/manifest.md) line and the [awaken](../0-the-void/awaken.md) line. Keep both markers, or Sentinel has nowhere to write.

## The trap: Keeper needs begin and end
Sentinel does **not** add `Keeper::begin()` and `Keeper::end()`. Without them, Keeper looks like it works — `Keeper::item()` returns `true` — but nothing is saved and no `.echoes` folder appears.

Add them by hand, inside the flow:

```php
Aether::begin();
Chanter::begin();
Keeper::begin();      // after Chanter::begin()

// …casts…

#sentinel-codex
Chanter::end();
Keeper::end();        // before Aether::end()
Aether::end();
```

What opens later closes earlier.

## Take a rune out
```bash
php cast sentinel --revoke=Cipher
```

Removes both lines again. `--invoke=Keeper.entity` and `--revoke=Keeper.essence` work on one part only.

Next: [Keeper](keeper.md).
