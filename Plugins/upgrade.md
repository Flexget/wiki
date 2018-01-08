# Upgrade
Upgrade plugin will continue getting better qualities of an entry (tracked by a unique identifier). It can also blocks any entry that are of a worse quality than you already have.

## Settings

| **Option** | **Description** |
| --- | --- |
| identified_by | Define how entries are identified, default `auto` which uses entry id field. Supports [Jinja Template](https://flexget.com/Jinja) |
| tracking | If enabled by it's self will track entry but not upgrade. |
| target | The target quality that should be upgraded to. Upgrades will not continue after target is met. |
| on_lower | action to preform. `allow` won't act on the entry (undecided) but allow it to by accepted by other plugins |
| timeframe | Allow upgrades for the given peroid of time |
| propers | Allow upgrade of same quality if proper is released |


## Syntax:

```code
upgrade:
  identified_by: <template>
  tracking: [yes|no]
  target: <quality requirement>
  on_lower: [accept|reject|allow]
  timeframe: <interval>
  propers: [yes|no]
```

## 

### Example for series


### Example for movies