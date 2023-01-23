---
title: Template
description: 
published: true
date: 2023-01-23T15:59:58.658Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:34.227Z
---

# Manage series easier with a template
With [template](/Plugins/template) plugin you can avoid having to duplicate configuration in multiple tasks. This can be adapted for movies, comics etc. easily. See [template](/Plugins/template) documentation for more tips.

```yaml
templates:
  tv:
    download: ~/torrents/series/
    exists_series: ~/storage/series/
    series:
      - pioneer one
      - south park

tasks:
  some-feed:
    rss: http://example.com/feed.xml
    template: tv

  another-feed:
    rss: http://foobar.com/feed.xml
    template: tv
```  

Uses plugins: [template](/Plugins/template), [rss](/Plugins/rss), [series](/Plugins/series), [exists_series](/Plugins/exists_series), [download](/Plugins/download)

[Back to The Cookbook](/Cookbook)