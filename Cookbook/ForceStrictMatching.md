---
title: ForceStrictMatching
description: 
published: true
date: 2022-09-18T05:27:40.112Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:26.237Z
---

# Force Exact Matching
Certain times, when using [configure_series](/Plugins/configure_series) you might want to force FlexGet into exact matching for a TV series.

## An Example
Say a user follows a series named Seriesname, this series is broadcasted in national versions in several countries. Thus the series that exist are:

* Seriesname
* Seriesname UK

By default FlexGet will consider both of these series the same, if 'Seriesname' is the title provided by configure_series.

## The Workaround
To solve this we can manually specify [exact](/Plugins/series/exact) mode for this series using the regular [series](/Plugins/series) plugin.

```
# Use configure_series as normal, and also include the series plugin like this:
series:
  # The series name specified here should be exactly the same as it comes from configure_series
  - Seriesname:
      exact: yes
```
The exact option will be merged into this specific series, along with any options you have specified for all series using configure_series plugin.