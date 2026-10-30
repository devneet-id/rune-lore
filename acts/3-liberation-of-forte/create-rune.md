# Create a Rune

> Sentinel shapes the empty rune for you.

A rune begins as a name and five empty files. Sentinel carves them; you engrave them.

## Create
In liberation mode:
```bash
php cast sentinel --create-rune=ledger
```
```
SENTINEL :: Create Rune
[√] Success create rune: Ledger
```
Without a name (`--create-rune`), Sentinel asks: *Give us the rune name:*

## What you get
```
@liberations/
├── README.md
└── Ledger/
    ├── Ether.php       define('LEDGER', true);
    ├── Essence.php     $GLOBALS['LEDGER'] = true;
    ├── Entity.php      function ledger() { return true; }
    ├── Manifest.php    class Rune\Ledger\Manifest extends \Rune\Manifest
    └── Phantasm.php    version 0.1 · main Ledger · mark BETA
```
A new rune is marked **BETA**, at version **0.1**. Its Phantasm joins the footer at once:
```
◇Version=1.20.110   before
◇Version=1.20.111   after --create-rune (major 0 → middle +0, minor 1 → last +1)
```

## Names
- The name is written `Ucfirst`: `ledger`, `LEDGER`, `Ledger` → `Ledger`.
- An origin name is refused:
  ```
  [!] 'Whisper' is an origin rune, use another name (e.g. MYWhisper).
  ```
- **Known issue:** the suggested `MYWhisper` becomes `Mywhisper` (the name is lowered, then the first letter raised). Pick a name that reads well in `Ucfirst`, like `Ledger` or `Echobook`.

## Remove
```bash
php cast sentinel --remove-rune=ledger
```
The folder is deleted **and** the rune is revoked from your runite, so no `use` line points to nothing. There is no undo — commit first.

Next: [Engrave a Rune](engrave-a-rune.md).
