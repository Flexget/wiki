## `series`
View and manipulate the series plugin database

### Actions
| argument | option | description |
| --- | --- | --- |
| `list`* || List a summary of the different series being tracked |
|| *positional:*|
||`{configured,unconfigured,all}` | Limit list to series that are currently in the config or not (default: configured) |
|| *optional:* |
|| `--premieres` | limit list to series which only have episode 1 (and maybe also 2) downloaded |
|| `--new [DAYS]` | Limit list to series with a release seen in last 7 days. number of days can be overridden with DAYS |
|| `--stale [DAYS]` | Limit list to series which have not seen a release in 365 days. number of days can be overridden with DAYS |
|| `--sort-by {name,age}` | Choose list sort attribute |
|| `--descending` | Sort in descending order |
|| `--ascending` | Sort in ascending order |
| `show`* || Show the releases FlexGet has seen for a given series |
|| *positional:*|
|| `<series name>` | The name of the series |
| `begin`|| set the episode to start getting a series from |
|| *positional:*|
|| `<series name>` | The name of the series |
|| `episode_id` | episode ID to forget (optional)|
| `forget`|| Removes episodes or whole series from the entire database (including seen plugin) |
|| *positional:*|
|| `<series name>` | The name of the series |
|| `episode_id` | episode ID to forget (optional)|
| `remove` || Removes episodes or whole series from the series database only |
|| *positional:*|
|| `<series name>` | The name of the series |
|| `episode_id` | episode ID to forget (optional)|
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||

### Examples
```bash
#lists a summary of the different series being tracked
flexget series list
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [series Plugin](/Plugins/series)