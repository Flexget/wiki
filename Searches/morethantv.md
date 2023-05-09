---
title: morethantv
description: 
published: true
date: 2023-05-09T15:30:03.508Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:13.140Z
---

# Morethantv
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get results from [https://www.morethantv.me/](https://www.morethantv.me/), also known as MTV.

## Configuration
Requires username and password. (your usual login credentials)
```
morethantv:
  username: xxxxxxx
  password: xxxxxxx
  category: TV
  all_tags: yes #match no matter what tag the search results have
```

**Categories**
- HD Episode
- HD Movies
- HD Season
- SD Epiosde
- SD Movies
- SD Season

**Tags**

*action, adventure, animation, anime, art, asian, biography, celebrities, comedy, cooking, crime, cult, documentary, drama, educational, elclasico, family, fantasy, film.noir, filmromanesc, food, football, formula.e, formula1, gameshow, highlights, history, horror, investigation, lifestyle, liga1, ligabbva, ligue1, martial.arts, morethan.tv, motogp, musical, mystery, nba, news, other, performance, philosophy, politics, reality, romance, romanian.content, science, scifi, short, silent, sitcom, sketch, sports, talent, tennis, thriller, uefachampionsleague, uefaeuropaleague, ufc, war, western, wta*

Tags are what you'd expect from defining a typical genre that you wish to get entries from. Use case would likely be for more generic downloading and not targeting specific shows/movies.

Normally, you'd just want to use `all_tags: yes`

## Usage
Say you want to perform a search on mtv using your [input](/Plugins) entries, and the entries are all TV shows. You can do that using the [discover](/Plugins/discover) plugin.

```
discover:
  what:
    - next_series_episodes: yes
  from:
    - morethantv:
        username: '{? mtv.username ?}'
        password: '{? mtv.password ?}'
        category:
          - HD Episode
        all_tags: yes
```

## Misc.
Morethantv plugin includes extra information about torrents in the search result, letting you access them in your config.

* torrent_internal (boolean)
* torrent_fast_server (boolean)
* torrent_sticky (boolean)
* torrent_tags