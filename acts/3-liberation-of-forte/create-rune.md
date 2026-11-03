# Create a Rune

> Sentinel shapes the empty rune for you.

A rune begins as a name and five empty files. Sentinel carves them; you engrave them.

## Create
In liberation mode:
```bash
php cast sentinel --runic-create=Ledger
```
```
SENTINEL :: Runic Create
[√] Rune created: @liberation/Ledger
```
Without a name (`--runic-create`), Sentinel asks: *Give us the rune name:*

## What you get
```
@liberation/
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
◇Version=1.20.114   before
◇Version=1.20.115   after --runic-create (major 0 → middle +0, minor 1 → last +1)
```

## Names
- A PascalCase name is kept as you write it: `Ledger`, `EchoBook`. Any other is written `Ucfirst`: `ledger`, `LEDGER` → `Ledger`.
- An origin name is refused:
  ```
  [!] 'Whisper' is an origin rune, use another name (e.g. MyWhisper).
  ```
- A rune that already exists is not created again.

## Delete
```bash
php cast sentinel --runic-delete=Ledger
```
The folder is deleted **and** the rune is removed from your runite, so no `use` line points to nothing. There is no undo — commit first.

Next: [Engrave a Rune](engrave-a-rune.md).
