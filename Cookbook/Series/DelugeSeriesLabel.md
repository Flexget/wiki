---
title: DelugeSeriesLabel
description: 
published: true
date: 2022-09-18T05:20:35.292Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:32.712Z
---

# Deluge labels based on series name
**NOTE:** As of r1840 this recipe is not needed as the [deluge](/Plugins/deluge) plugin will replace any invalid characters in the label name with '_' automatically. Also, the [set](/Plugins/set) plugin can now be used to make this sort of replacement much easier.

Deluge does not support spaces in label names, so this has to be worked around in order to have automatic labels based on series names. This can be accomplished by using the [manipulate](/Plugins/manipulate) plugin to create the label from series name with spaces replaced by underscores. We also need to use [plugin_priority](/Plugins/plugin_priority) to make the manipulate plugin run after [series](/Plugins/series), so that series has a chance to populate the [series_name field](/Entry#Knownfields).
```
feeds:
  tv:
    rss: http://feed.com/feed
    series:
      - Series One
      - Series Two
    manipulate:
      - label:
          from: series_name
          replace:
            regexp: ' '
            format: '_'
    plugin_priority:
      manipulate: 0
    deluge: yes
```