---
title: SimpleEbooks
description: 
published: true
date: 2022-09-18T05:10:39.625Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:15.649Z
---

# Simple Ebook Recipes
# Using download plugin
This recipe uses the regexp plugin to download torrents from an rss feed to a specified path.

```
tasks:
  books:
    rss: http://example.com
    regexp:
      accept:
        - Some Publisher
        - Some Magazine
    download: /path/to/torrents/
```

Uses plugins:  [regexp](/Plugins/regexp),[download](/Plugins/download)