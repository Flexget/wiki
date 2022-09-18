---
title: all_series
description: 
published: true
date: 2022-09-18T05:12:42.022Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:55.012Z
---

# All Series
Automatically configures the [series](/Plugins/series) plugin for all series that appear in the feed.

Plugin expects the title format to start with the series name followed by the episode numbering. Use the [manipulate](/Plugins/manipulate) plugin to modify the entry title to match this format, if necessary. Since it's very hard to guess series names you're much more likely to get significantly more robust matching (and thus downloading) with configuring [series](/Plugins/series) plugin with **explicit** series names. You can also mix and match all different configuration methods.

### Example

Turns on the plugin for a task.

```
all_series: yes
```

## Settings
Behind the scenes, `all_series` just configures the [series](/Plugins/series) plugin with all the series it sees in the task. You can use any of the [settings](/Plugins/series#Settings) of the series plugin for all_series.

### Example

```
all_series:
  path: /media/TV
  quality: 720p hdtv
  propers: no
```
You can use [`--dump-config` ](/CLI/execute) option to see generated configuration file. You will likely only want to execute single task when doing that.