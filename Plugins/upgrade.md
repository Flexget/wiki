# Upgrade
Upgrade plugin will continue getting better qualities of an entry (tracked by a unique identifier). It can also blocks any entry that are of a worse quality than you already have.

## Settings
The series plugin supports a number of settings to customize it's behavior. Though the examples show the settings being applied to a single series, they can all be applied to a group of series as well.

[How to configure settings per series](/Plugins/series/per_series_settings)  
[How to configure settings with groups](/Plugins/series/per_group_settings)


| **Option** | **Description** |
| --- | --- |
| identified_by | Define how entries are identified, default `auto` which uses entry id field. |
| tracking | If enabled by it's self will track entry but not upgrade. |
| target | The target quality that should be upgraded to. Upgrades will not continue after target is met. |
| on_lower | action to preform |
| timeframe | Allow upgrades for the given peroid of time |
| propers | Allow upgrade of same quality if proper is released |


### Example
TBC