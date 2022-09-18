---
title: next_trakt_episodes
description: 
published: true
date: 2022-09-18T05:12:57.326Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:08:48.136Z
---

# Next Trakt Episodes
<div class="alert alert-info" role="alert">

Please see [Trakt Authentication](/Trakt_Authentication) for how to authorize FlexGet to access your Trakt.tv account.
</div>

<div class="alert alert-danger" role="alert">
Warning: There is currently a problem where this plugin will not emit the next episode for a season when it has not yet aired. #2831
</div>

This plugin creates an [Entry](/Entry) for the next episode to watch or to collect for each show you have marked seen or collected in your [trakt.tv](http://trakt.tv) account.

This plugin can be used in combination with several plugins, like [discover](/Plugins/discover) to search for new episodes to download, or [set_series_begin](/Plugins/set_series_begin) to reset the first episode for configured series, and so on.  

## Plugin Settings
Currently the following settings are supported:



| **Option** | **Description** |
| --- | --- |
| **username** | This is your username at [trakt.tv](http://trakt.tv)  |
| **account** | Your account name set during [Trakt authentication](/Trakt_Authentication). **Required** if the list is private. |
| **context** | Can be **watched** (default), **collected**, or **aired**. It refers to the seen and collected status for your account on Trakt. |
| **position** | Can be **next** (default) or **last**. Combined with the `context` option, this instructs the plugin to emit the next episode to watch, the next episode to collect, the last episode watched or the last episode collected for each series. |
| **list** | The name of a Trakt custom or built-in list to limit the series for which to emit entries. |
| **strip_dates** | If set to `yes` the year will be removed from the end of titles that contain them.  (Note 1: as of 2017, Trakt includes the year in the title of _all_ television series, even those that wouldn't ordinarily need them to distinguish from another series. This option removes years from _all_ series titles. Note 2: To search and accept series that do not have release year in the series title, the Discover plugin needs this set to `yes` unless you set the beginning of an episode manually. The search plugins will still search series with and without release year.


### Example: set series begin
This example shows how the next_trakt_episodes plugin could be used with the [set_series_begin](/Plugins/set_series_begin) plugin in order to set the first episode to download for the series in the my_tv_show list on Trakt. By default FlexGet will start from first episode it sees in the task. This is mainly useful if you set up discover.

```
tasks:
  sync-trakt:
    next_trakt_episodes:
      account: your_account
      context: collected
      list: my_tv_show
    accept_all: yes
    set_series_begin: yes
```

  
**Notes:**

Trakt will not emit any info for series the user has never marked seen or collected, even if the **list** option is used and the actual custom list contains them. However, when this situation occurs, the plugin will emit a default S01E01 episode id, but only with the **list** option and **position**=**next**.