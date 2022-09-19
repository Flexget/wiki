---
title: series
description: 
published: true
date: 2022-09-18T05:12:42.022Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:29.061Z
---

## [CLI](/CLI) > `series`
View and manage the [`series` plugin](/Plugins/series) database.

### Sub-commands
| Sub-command                                                           | Option | Description/Example|
|-----------------------------------------------------------------------| --- | --- |
| `list`<a name="subcommand-list"></a>[*](#TableStylesDiv)            || List a summary of the different series being tracked |
|| `(configured                                                          |unconfigured|all)`[^†^](#EnvDiv) | Limit list to series that are currently in the config or not (default: configured)
|| `--premieres`[^†^](#EnvDiv)                                  | Limit list to series which only have episode 1 (and maybe also 2) downloaded |
|| `--new <days>`[^†^](#EnvDiv)                                 | Limit list to series with a release seen in last 7 days. number of days can be overridden with DAYS |
|| `--stale <days>`[^†^](#EnvDiv)                               | Limit list to series which have not seen a release in 365 days. number of days can be overridden with DAYS |
|| `--sort-by (name                                                      |age)`[^†^](#EnvDiv) | Choose list sort attribute
|| `--descending`[^†^](#EnvDiv)                                 | Sort in descending order |
|| `--ascending`[^†^](#EnvDiv)                                  | Sort in ascending order |
| `show`<a name="subcommand-show"></a>[*](#TableStylesDiv) || Show the releases FlexGet has seen for a given series | 
|| `<series name>`                                                       | Name of the series
|| `--sort-by (age                                                       |identifier)`[^†^](#EnvDiv) | Choose list sort attribute |
|| `--descending`[^†^](#EnvDiv)                                 | Sort in descending order |
|| `--ascending`[^†^](#EnvDiv)                                  | Sort in ascending order |
| `begin`                                                               || Set the episode to start getting a series from (use `forget` to remove it) |
|| `<series name>`                                                       | Name of the series |
|| `<episode_id>`                                                        | Episode or season ID to start getting the series from (e.g. S02E01, 2013-12-11, or 9, depending on how the series is numbered, or S02 for season)|
| `forget`                                                              || Removes episodes, seasons, or a whole series from the entire database (including [`seen`](/Plugins/seen) plugin) |
|| `<series name>`                                                       | Name of the series |
|| `<episode_id> [<episode_id> ...]`<br>`<season_id> [<season_id> ...]`  | Episode or season ID(s) to forget (optional)
| `remove`                                                              || Removes episodes, seasons, or a whole series from the series database only |
|| `<series name>`                                                       | Name of the series |
|| `<episode_id> [<episode_id> ...]`<br>`<season_id> [<season_id> ...]`  | Episode or season ID(s) to forget (optional)||
| `add`<a name="subcommand-add"></a>                                    |||
|| `<series name>`                                                       | Name of the series |
|| `<episode_id> [<episode_id> ...]`<br>`<season_id> [<season_id> ...]`  | Episode or season ID(s)  to add
|| `--quality <quality_string>`[^†^](#EnvDiv)                   | [Quality](/Plugins/quality#qualities) string that is attached to each entity added
[Includes/TableStylesDiv](/Includes/TableStylesDiv){.include}
[Includes/EnvDiv](/Includes/EnvDiv){.include}


### Environment Variables
Environment variables set option defaults for the subcommand noted, and are overridden by the corresponding flag(s) listed.
| Subcommand | Variable | Possible Values | Description | Corresponding Argument(s) |
| --- | --- | --- | --- | --- |
| `show`[&uarr;](#subcommand-show) |||||
| | `FLEXGET_SERIES_SHOW_SORTBY_FIELD` | `age`, `identifier` | Sort option for releases. | `--sort-by` |
| `list`[&uarr;](#subcommand-list) |||||
| | `FLEXGET_SERIES_SHOW_SORTBY_ORDER` | `desc` | Reverses the sort order. | `--descending`<br>`--ascending` |
| | `FLEXGET_SERIES_LIST_CONFIGURED` | `configured`, `unconfigured`, `all` | Limit series displayed to those in the config or not. | positional:<br>`configured`<br>`unconfigured`<br>`all` |
| | `FLEXGET_SERIES_LIST_PREMIERES` | `yes` | Limit series displayed to those with a maximum of two episodes downloaded. | `--premieres`
| | `FLEXGET_SERIES_LIST_STATUS` | `new`, `stale` | Limit series displayed those with a release in the last 7 days (`new`) or without a release in the last 365 days (`stale`). The number of days can be customized with `FLEXGET_SERIES_LIST_NUMDAYS`. | `--new`<br>`--stale` |
| | `FLEXGET_SERIES_LIST_NUMDAYS` | integer | The number of days used in the calculation for `new` or `stale` status. | `<days>` after `--new` or `--stale`
| | `FLEXGET_SERIES_LIST_SORTBY_FIELD` | `name`, `age` | Sort option for series. | `--sort-by` |
| | `FLEXGET_SERIES_LIST_SORTBY_ORDER` | `desc` | Reverses the sort order. | `--descending`<br>`--ascending` |
| `add`[&uarr;](#subcommand-add) |||||
| | `FLEXGET_SERIES_ADD_QUALITY` | [quality](/Plugins/quality#qualities) string | The quality that is attached to each entity added | `--quality <quality_string>` |


### Examples
```bash
#lists a summary of the different series being tracked
$ flexget series list

#sets the series "FooSeries" to start with episode one of season 6
$ flexget series begin FooSeries S06E01

#shows all releases for the show FooSeries
$ flexget series show FooSeries

#deletes the whole show FooSeries even from seen plugin
$ flexget series forget FooSeries
```