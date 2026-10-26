# Engrave a Rune

> Fill the five files: one rune, one purpose.

<!-- status: draft -->

A rune does one thing well. **Ledger** keeps a small book of income and expense in one flow — nothing else. Before you write code, say its purpose in one sentence. If you need *and*, you may need two runes.

Every name carries the rune's name, so it never collides with another rune:

| Subject | Holds | Name |
|---|---|---|
| Ether | constants — truth that never changes | `LEDGER_*` |
| Essence | globals — state of this flow | `$LEDGER_*` |
| Entity | functions — the logic | `ledger_*()` |
| Manifest | the static face your runite calls | `Ledger::name()` |

Write `#NOTE:` above every constant, global, function and method. Sentinel copies these notes into the [Phantasm](phantasm.md), and the Grimoire shows them.

## Ether.php
```php
<?php

/*
 * ETHER
 * Represents constants and rules for this domain.
 */

#NOTE: Acts as a flag to indicate that the LEDGER system is enabled.
define('LEDGER', true);

#NOTE: The currency written before every amount.
define('LEDGER_CURRENCY', 'IDR');

#NOTE: The template of one ledger line.
define('LEDGER_LINE', '{{sign}} {{currency}} {{amount}}  {{note}}');
```

## Essence.php
```php
<?php

/*
 * ESSENCE
 * Represents globals and base data for this domain
 */

#NOTE: Every entry written in this flow.
$GLOBALS['LEDGER_ENTRIES'] = [];
```

## Entity.php
The logic lives here. An entity may call the entities of other runes — that is how runes lean on each other. `ledger_line()` weaves with Weaver.
```php
<?php

/*
 * ENTITY
 * Represents functions related to this domain.
 */

#NOTE: Adds one entry (positive = income, negative = expense) and returns the entry count.
function ledger_add( Float $amount, String $note = '' ) {
  global $LEDGER_ENTRIES;
  $LEDGER_ENTRIES[] = ['amount' => $amount, 'note' => $note];
  return count($LEDGER_ENTRIES);
}

#NOTE: Returns the sum of every entry.
function ledger_total() {
  global $LEDGER_ENTRIES;
  return array_sum(array_column($LEDGER_ENTRIES, 'amount'));
}

#NOTE: Weaves one entry into a line of text.
function ledger_line( Array $entry ) {
  return weaver_bind_multiple(LEDGER_LINE, [
    'sign' => $entry['amount'] < 0 ? '-' : '+',
    'currency' => LEDGER_CURRENCY,
    'amount' => number_format(abs($entry['amount'])),
    'note' => $entry['note'],
  ], false);
}
```

## Manifest.php
The Manifest only forwards to the entities, and leaves a trace in the [arcane](../2-understanding-its-flow/arcane.md) with `aether_arcane('Rune.manifest.method')`.
```php
<?php

/*
 * MANIFEST
 * Represents the main static controller for this domain.
 */

namespace Rune\Ledger;

class Manifest extends \Rune\Manifest {

  protected static $origin = __DIR__;

  #NOTE: Adds one entry to the ledger.
  public static function add( Float $amount, String $note = '' ) {
    $return = ledger_add($amount, $note);

    aether_arcane('Ledger.manifest.add');
    return $return;
  }

  #NOTE: Returns the total of the ledger.
  public static function total() {
    $return = ledger_total();

    aether_arcane('Ledger.manifest.total');
    return $return;
  }

  #NOTE: Returns every entry as woven lines.
  public static function lines() {
    global $LEDGER_ENTRIES;
    $return = array_map('ledger_line', $LEDGER_ENTRIES);

    aether_arcane('Ledger.manifest.lines');
    return $return;
  }

}
```
The generated Manifest also has an empty `_arise()`. It is a legacy hook that Aether no longer calls — keep it or drop it. If your rune must open and close with the flow, give it `begin()` / `end()` and call them from the runite, like Keeper.

## Use it once
```php
Chanter::cast('month', function() {
  Ledger::add(5000000, 'salary');
  Ledger::add(-1250000, 'rent');
  Ledger::add(-300000, 'internet');
  foreach (Ledger::lines() as $line) Whisper::echo("$line{{nl}}");
  Whisper::echo("{{color-success}}= " . LEDGER_CURRENCY . ' ' . number_format(Ledger::total()) . "{{nl}}");
}, 'A month in the ledger.');
```
```
$ php cast month
+ IDR 5,000,000  salary
- IDR 1,250,000  rent
- IDR 300,000  internet
= IDR 3,450,000
```
(The runite must [invoke](use-your-rune.md) Ledger first.)

## The laws, again
- One rune, one purpose.
- Entity holds the logic; Manifest only forwards.
- Lean on origin runes through their entities — do not copy them.
- Keep state in Essence, not in static properties, so the Grimoire can see it.

Next: [Phantasm](phantasm.md).
