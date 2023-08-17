---
title: series
description: 
published: true
date: 2023-08-17T01:55:23.487Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:38.011Z
---

# Series
Intelligent filter for TV-series.

## Features
 * Episode history aware, no duplicate downloads - refer to [seen](/Plugins/seen) plugin page for more information
 * Plenty of [quality](/Plugins/series/quality) options
 * [Timeframe](/Plugins/series/timeframe), when used with sort_by plugin, selects the entry best matching the criteria in given timeframe
 * [Proper & Repack](/Plugins/series/propers) aware
 * Specials aware (grabs episodes with the series title and the word 'special')
 * Tries to ignore season packs, you can use [content_size](/Plugins/content_size) for extra insurance against them.
 * Supports double episodes. i.e. S01E01-E02
 * [Series searching support](/Cookbook/Series/Search) (via [discover](/Plugins/discover) and [next_series_episodes](/Plugins/next_series_episodes) plugins)

**Simple configuration:**

```
series:
  - some series
  - another series
```

If `some series` and `another series` have understandable episode
numbering any given episode is downloaded only once. FlexGet should support all known episode numbering schemes without any configuration, including dates.

So if we get same episode twice:

 * Some.Series.S2E10.720p.x264-FlexGet
 * Some.Series.S2E10.HR.x264-FooBar

Only one of them is downloaded, with default configuration the first entry matching quality requirements is chosen. To get the best quality within specified timeframe use the sort_by plugin in the task.

```
sort_by:
  field: quality
  reverse: yes
```

## Related plugins
These plugins are complementary to the series plugin.

| Name | Description |
| --- | --- |
| [all_series](/Plugins/all_series) | Grab all series in the task|
| [configure_series](/Plugins/configure_series) | Automatically configures series by using another input, some examples: [thetvdb_favorites](/Plugins/thetvdb_favorites), [trakt_list](/Plugins/List/trakt_list) and [filesystem](/Plugins/filesystem).<br> With this you don't need to maintain series configuration in the configuration file.  |
| [series_premiere](/Plugins/series_premiere) | Download all premieres| 
| [next_series_episodes](/Plugins/next_series_episodes) | Emit next episodes for [discover](/Plugins/discover) | 
| [next_series_seasons](/Plugins/next_series_seasons) | Emit next seasons for [discover](/Plugins/discover) | 


## Settings
The series plugin supports a number of settings to customize it's behavior. Though the examples show the settings being applied to a single series, they can all be applied to a group of series as well.

[How to configure settings per series](/Plugins/series/per_series_settings)  
[How to configure settings with groups](/Plugins/series/per_group_settings)


| **Option** | **Description** |
| --- | --- |
| [alternate_name](/Plugins/series/alternate_name) | Define other names which this show is also released as. |
| [assume_special](/Plugins/series/assume_special) | Assume any entry with no series numbering detected is a special and treat it accordingly. |
| [begin](/Plugins/series/begin) | Manually specify first episode to start series on. |
| [ep_regexp](/Plugins/series/regexps#Episodenumberingmatching) | Manually specify regexp(s) that matches to episode, season numbering. |
| [exact](/Plugins/series/exact) | Configure exact matching behavior. Needed for series which have similar named series. Uses 'auto' mode as default. |
| [from_group](/Plugins/series/from_group) | Accept series only from given groups. |
| [id_regexp](/Plugins/series/regexps#Episodenumberingmatching) | Manually specify regexp(s) that matches to series identifier (numbering). |
| [identified_by](/Plugins/series/identified_by) | Configure how episode numbering is detected. Uses 'auto' mode as default. |
| [name_regexp](/Plugins/series/regexps) | Manually specify regexp(s) that matches to series name. |
| [parse_only](/Plugins/series/parse_only) | Series plugin will not accept or reject any entries, merely fill in all metadata fields. |
| [path](/Plugins/series/path) | Set *path* field for this series. |
| [prefer_specials](/Plugins/series/prefer_specials) | Flag entries matching both special and a normal ID type as specials. |
| [propers](/Plugins/series/propers) | Configure how propers are handled. |
| [qualities](/Plugins/series/qualities) | Download all listed qualities when they become available. |
| [quality](/Plugins/series/quality) | Required quality. |
| [set](/Plugins/series/set) | Use [set](/Plugins/set) plugin to set any fields for this series. |
| [special_ids](/Plugins/series/special_ids) | Defines other IDs which will cause entries to be flagged as specials. |
| [specials](/Plugins/series/specials) | Turn off specials support for series. (on by default) |
| [target](/Plugins/series/timeframe) | The target quality that should be downloaded without waiting for `timeframe` to complete. |
| [timeframe](/Plugins/series/timeframe) | Wait given amount of time for specified quality to become available, after that fall back to best so far. |
| [upgrade](/Plugins/series/upgrade) | Keeps getting the better qualities as they become available. |
| [season_packs](/Plugins/series/season_packs) | Enable downloading season packs. 

#### Notes

* If the series appears in task(s) with slightly different naming conventions and spinoffs like FooBar and FooBar US read [this guide](/Plugins/series/closematch). 
* FlexGet respects *propers* which means that the same episode will be downloaded twice if the second one contains words such as `proper`, `repack`, `rerip`, or `real`.
* If series name is written in multiple different ways, don't add them as separate series. This will confuse episode tracking. 
* Check [series cookbook](/Cookbook/Series) for more complete examples and advanced uses.
* If using discover, existing collection can be imported with [this](/Cookbook/Series/SeedDB) recipe.

## `series` Commandline Arguments
The series plugin has several features available at the command line via the [`flexget series` command](/CLI/series).

## `execute` Commandline Arguments
There are also options to the `flexget execute` command which affect the series plugin:

Using `series begin` to set new starting point is recommended and should resolve any tracking issues. If you for some reason need to record episode into history it can be achieved with command `flexget inject "Pioneer One 05" --task <name> --learn`.


### \-\-stop-waiting \<name\>
Stops timeframe for given name, thus downloading any episode that is currently pending in the timeframe.