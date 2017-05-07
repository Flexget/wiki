## [CLI](/CLI) > `series`
View and manage the [`series` plugin](/Plugins/series) database.

### Sub-commands
| Sub-command | Option | Description/Example|
| --- | --- | --- |
| `list`* || List a summary of the different series being tracked |
||`(configured|unconfigured|all)` | Limit list to series that are currently in the config or not (default: configured)
|| `--premieres` | Limit list to series which only have episode 1 (and maybe also 2) downloaded |
|| `--new <days>` | Limit list to series with a release seen in last 7 days. number of days can be overridden with DAYS |
|| `--stale <days>` | Limit list to series which have not seen a release in 365 days. number of days can be overridden with DAYS |
|| `--sort-by (name|age)` | Choose list sort attribute
|| `--descending` | Sort in descending order |
|| `--ascending` | Sort in ascending order |
| `show`* || Show the releases FlexGet has seen for a given series | 
|| `<series name>` | Name of the series
| `begin`|| Set the episode to start getting a series from (use `forget` to remove it) |
|| `<series name>` | Name of the series |
|| `<episode_id>` | Episode ID to start getting the series from (e.g. S02E01, 2013-12-11, or 9, depending on how the series is numbered)|
| `forget`|| Removes episodes, seasons, or a whole series from the entire database (including [`seen`](/Plugins/seen) plugin) |
|| `<series name>` | Name of the series |
|| `<episode_id>`/`<season_id>` | Episode or season ID(s) to forget (optional)
| `remove` || Removes episodes, seasons, or a whole series from the series database only |
|| `<series name>` | Name of the series |
|| `<episode_id>`/`<season_id>` | Episode or season ID(s) to forget (optional)||
|||<div align="right">* supports <a href="/CLI/--table-styles">table-styles</a></div>|

### Examples
```bash
#lists a summary of the different series being tracked
flexget series list
#sets the series "FooSeries" to start with episode one of season 6
flexget series begin FooSeries S06E01
#shows all releases for the show FooSeries
flexget series show FooSeries
#deletes the whole show FooSeries even from seen plugin
flexget series forget FooSeries
```