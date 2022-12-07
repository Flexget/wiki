---
title: cpasbien
description: 
published: true
date: 2022-12-07T05:43:29.415Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:17:18.576Z
---

> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

>As cpasbien switched to cloudflare, some tweaks are required
You have to have https://github.com/Anorov/cloudflare-scrape and all it's dependency to make it work.
Additionally, the file cfscrape.py must be put in the folder : /var/lib/flexget
{.is-danger}

# CPASBIEN Search plugin
This search plugin will get results from [http://www.cpasbien.pw/](/http://www.cpasbien.pw/)

## Configuration
Configuration requires only the category and you can only have ONE:
```
cpasbien: <category>
```


| **Category** | **Description** |
| --- | --- |
| all | Not filtered by any category |
| misc | Category for miscellaneous files |
| films | Main category for movies & other videos |
| films-french | Main category for french movies |
| 1080p | Main category for 1080p movies |
| 720p | Main category for 720p movies |
| films-french | Main category for french movies |
| films-dvdrip | Main category for dvdrip movies |
| films-vostfr | Main category for movies in English sub French |
| series | Category for tv shows |
| series-francaise | Category for tv shows in french |
| series-vostfr | Category for tv shows in English sub French |
| ebook | Category for books |
| musique | Category for music |

Example with discover:
```
tv_search_cpasbien:
  discover:
    what:
      - trakt_list:
          username: xxxxxxx
          list: watchlist
          type: shows
    from:
      - cpasbien:
          category: series-vostfr
    interval: 1 day
    ignore_estimations: yes
```

