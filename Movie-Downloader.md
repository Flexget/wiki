---
title: Movie-Downloader
description: 
published: true
date: 2022-09-18T04:50:47.902Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:50:45.354Z
---



```
tasks:
  watchlist:
    priority: 1
    trakt_list:  
      account: asljasfh
      list: movies
    accept_all: yes
    seen: local
    list_add:
      - movie_list: movies

  # task that automatically downloads movies from the movie_list
  movies search:
    trakt_lookup: yes
    priority: 10 
    discover:
      what:
        - movie_list: movies
      from:
        - piratebay: yes
      interval: 7 days
    torrent_alive: 10 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
    content_size:
      min: 12
      max: 2500
  strict: no
    list_match:
      from:
        - movie_list: movies
    download: Users/petersterling/Desktop/torrents
```