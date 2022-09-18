---
title: Sort
description: 
published: true
date: 2022-09-18T05:21:32.912Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:30.299Z
---

# Sort downloads
This recipe is to sort your already downloaded series into their own folders. Note that FlexGet is not really made for sorting so this is a bit complicated and hackish.

```
templates:

  # NOTE!! This template cannot have any other plugins or else it will affect our sort-series.
  # Also, you must use series groups, so that we can turn off filtering with the parse_only option in our sort feed.
  tv-series:
    series:
      agroup:
        - Chuck
        - Eureka
        - Big Bang Theory
        - True Blood
        - Dollhouse
        - House
        - Persons Unknown
  
tasks:

  download-rss:
    rss: ...
    template:
      - tv-series
    download: ...

  sort-series:
    filesystem:
      path: /storage/downloads/
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    seen: local
    template: tv-series
    # NOTE: You must set the parse_only option for all of the series groups you have configured in your template.
    # This option prevents the series plugin from accepting or rejecting anything in this feed.
    series:
      settings:
        agroup:
          parse_only: yes
    # Ignore samples
    regexp:
      reject: 
        - sample
    # With the require_field and accept_all plugins, we accept anything that the series plugin has successfully parsed.
    require_field: series_name
    accept_all: yes
    move:
      to: /storage/series/{{series_name}}/Season {{series_season|pad(2)}}
```
**Uses Plugins:**

 - [filesystem](/Plugins/filesystem): In this recipe, we use filesystem which creates an entry for each file in the specified path (/storage/downloads/ in this case,) that match the regexp pattern specified.
 - [seen](/Plugins/seen): The seen plugin is enabled by default on all tasks, however we need to enable local mode to make sure that entries are not rejected because they were already seen in our normal download task.
 - [series](/Plugins/series): The series plugin is used to grab the series info (name, season, episode) from each file. We must list out all the series we want sorted.
 - [Plugins/require_field](/Plugins/require_field): Require series to be parsed successfully
 - [regexp](/Plugins/regexp): Ignore samples
 - [move](/Plugins/move): We use the move plugin to move the file to a dynamic path based on the parsed series name and season. If there are other files in the input directory that the series plugin cannot parse, they will be skipped and remain in the original directory.


[Back to The Cookbook](/Cookbook)