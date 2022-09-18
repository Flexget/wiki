---
title: TimeframeWithMinMaxQuality
description: 
published: true
date: 2022-09-18T05:21:40.554Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:38.004Z
---

# Series timeframe with min and max quality
The [series](/Plugins/series) plugin supports defining a min and max quality along with [timeframe](/Plugins/series#Timeframe) option.
```
series:
  settings:
    groupa:
      min_quality: hdtv
      max_quality: 720p web-dl
      quality: 720p
      timeframe: 12 hours
  groupa:
    - The Show
```
 ^^^(This config snippet must be placed within a feed or a preset.)^^^
This example will download a `720p` copy of `The Show` as soon as it comes out in the feed. If a quality within the range set by min_ and max_quality comes out before a `720p` copy, the [series](/Plugins/series) plugin will wait `12 hours` for the `720p` version before grabbing the alternative instead.
    
