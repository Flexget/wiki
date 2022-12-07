---
title: rarbg
description: 
published: true
date: 2022-12-07T05:20:10.628Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:36.271Z
---

# RarBG
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get results from [http://rarbg.com](http://rarbg.com)

## Configuration
You can search in a single category:
```yaml
rarbg: 
  category: x264 1080p
```

or in multiple categories:
```yaml
rarbg: 
  category:
    - x264 720p
    - x264 1080p
```

## List of possible categories
* `x264 720p`
* `x264 1080p`
* `XviD`
* `Full BD`
* `HDTV`
* `SDTV`

**Advanced:** You can also use categories ID directly, you can find them on RarBG if you hover over category link. (eg. rarbg.com/torrents.php?**category[]=45**). Multiple categories are separated by semi-colons in the url.
```
rarbg: 
  category: 2
```
Or multiple category IDs:
```
rarbg: 
  category: [2, 5, 8, 9, 20, 15, 16]
```

## Other settings
* `sorted_by`: `seeders`, `leechers` or `last`. Defaults to `last` ie. sorted by newest.
* `limit`: number of torrents, supports 25, 50 or 100.
* `ranked`: `True` or `False`. Defaults to `True`, which means it will only show RarBG related torrents ie. yify releases are ignored.
* `use_tvdb`: `True` or `False`. Defaults to `False`. This setting will fetch the tvdb id for the tv show in question and use it to find better matches. Without this setting enabled, the plugin will only search in the latest 10000 uploads, which means old stuff won't show up in the search results.
* `min_leechers`: Minimum number of leechers.
* `min_seeders`: Minimum number of seeders.