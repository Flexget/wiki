---
title: HeroesComics
description: 
published: true
date: 2022-09-18T05:14:07.567Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:33.866Z
---

# Download Heroes comics
Download all/new heroes comics from [nbc.com](http://nbc.com/Heroes). This uses advanced text-parsing plugin and does not represent accurately average usage.

```
feeds:
  heroes:
    interval: 6 hours
    text:
      url: http://www.nbc.com/Heroes/js/novels.js
      entry:
        title: novelTitle = "(.*)"
        url: novelPrint = "(.*)"
      format:
        url: http://www.nbc.com%(url)s
    download: ~/heroes/
```

Uses plugins: [interval](/Plugins/interval), [text](/Plugins/text), [download](/Plugins/download)

[Back to The Cookbook](/Cookbook)