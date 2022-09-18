---
title: MakeRssForDownload
description: 
published: true
date: 2022-09-18T05:14:03.735Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:48.858Z
---

# Make download RSS
This will produce rss-feed containing all matches with direct downloadable urls (resolved). This is useful if you wish to hook up FlexGet with a client that does not have a [watch directory](/WatchDirectory) support, or if you wish to perform downloading in a another computer. Only downside is that you need a HTTP server like Apache to host the RSS-feed.

```
templates:
  global:
    make_rss:
      link: url
      file: ~/public_html/flexget.rss

feeds:
  some feed:
    regexp:
      accept:
        - example

  another feed:
    series:
      - some series
```

Uses plugins: [template](/Plugins/template), [make_rss](/Plugins/make_rss)

[Back to The Cookbook](/Cookbook)

