---
title: Movie-Search
description: 
published: true
date: 2022-09-18T05:25:06.944Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:50:49.043Z
---



  
  ```
  movies search:
    trakt_lookup: yes  # can also use imdb_lookup or tmdb_lookup
    priority: 10 # run after the movie queue fill task
    discover:
      what:
        - movie_list: watchlist
      from:
        - piratebay: yes
      interval: 7 days
    torrent_alive: 10 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
    list_match:
      from:
        - movie_list: watchlist
    transmission: yes # You could use another output plugin instead of this (deluge, download)
```
    
  Plugins used: [movie_list](/Plugins/List/movie_list),  [trakt_lookup](/Plugins/trakt_lookup),[transmission](/Plugins/transmission),[accept_all](/Plugins/accept_all), [movie_list](/Plugins/List/movie_list), [list_match](/Plugins/List/list_match), [seen](/Plugins/seen), [torrent_alive](/Plugins/torrent_alive),[priority](/Plugins/priority),[discover](/Plugins/discover),[search plugin](/Searches) [piratebay](/Searches/piratebay).