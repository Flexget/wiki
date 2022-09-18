---
title: publichd
description: 
published: true
date: 2022-09-18T05:18:34.982Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:32.385Z
---

# publichd
{{> Includes/PluginRemovedArchived }}

This search plugin will get results from [http://publichd.se](/http://publichd.se)

## Configuration
You can search only single category:
```
publichd: 
  category: BluRay 1080p
```

Or for searching multiple categories:
```
publichd: 
  category:
    - BluRay 720p
    - BluRay 1080p
```

## List of possible categories
* `BluRay 720p`
* `BluRay 1080p`
* `XviD`
* `BRRip`
* `HDTV`
* `SDTV`
* `TV WEB-DL`

**Advanced:** You can also use categories ID directly, you can find them on PublicHD if you hover over category link. (eg. publichd.se/index.php?page=torrents&**category=2**)
```
publichd: 
  category: 2
```
Or multiple category IDs:
```
publichd: 
  category: [2, 5, 8, 9, 20, 15, 16]
```