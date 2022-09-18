---
title: Advanced
description: 
published: true
date: 2022-09-18T05:20:19.903Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:17.440Z
---

# Advanced example
How to use most of the series plugin features, with template:

```
templates:
  tv:
    series:
      settings:
        720p:
          timeframe: 12 hours

      720p:
        - house
        - chuck 
 
      normal:
        - the colbert report

    download: ~/watch/torrent/series/

feeds:
  my-feed-a:
    rss: http://example.com/feed-a.rss
    template: tv

  my-feed-b:
    rss: http://example.com/feed-b.rss
    template: tv

```