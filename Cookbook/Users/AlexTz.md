---
title: AlexTz
description: 
published: true
date: 2022-09-18T05:22:31.493Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:28.954Z
---

This is the personal configuration of user AlexTz . 

This is a complete work in progress.



```
templates:
  global:
#download path
    download: /path/to/utorrent/watch/folder/
#receiving iphone notifications through prowl when something new has been added
    prowl:
      apikey: apikey 
      application: Flexget
      priority: -2
#don t want no archives
    content_filter:
      require:
        - '*.avi'
        - '*.mkv'
        - '*.mp4'
#adding new series to trakt collections
  trakt_seen_series:
    trakt_acquired: 
      username: user
      password: pass
      api_key: key
      type: series

#adding new movies to trakt collections
  trakt_seen_movies:
    trakt_acquired: 
      username: user
      password: pass
      api_key: key
      type: movies

#importing series from trakt series watchlist  
  tv:
    import_series: 
      from:
        trakt_list:
          username: user
          password: pass
          api_key: key
          series: watchlist
      settings:
        propers: yes
        timeframe: 24 hours
        target: 720p+ hdtv+
        identified_by: ep

#filtering stuff in the hd movies rss feed through imdb to see if there is anything worth seeing 
  movies_imdb_filter: 
    imdb:
      min_score: 7.0
      min_votes: 5000
      min_year: 2011
      reject_genres:
        - horror
        - documentary
        - musical
        - music
        - biography
    quality: 1080p
    seen_movies: loose

#populating the movie_queue from the trakt watchlist
  trakt_movies_input:
    trakt_list:
      username: user
      password: pass
      api_key: key
      movies: watchlist
    queue_movies:
      quality: 1080p
      force: no
    imdb_lookup: yes
    accept_all: yes


tasks:
#populating movie_queue
  moviesFromTrakt: 
    priority: 1
    template: 
      - no_global
      - trakt_movies_input

#getting the series rss      
  freshonTV:
    rss: http://series.private.tracker
    template:
      - tv
      - trakt_seen_series
    priority: 10

#gettign the movies rss        
  filelistMoviesHD:
    priority: 30
    rss: http://movies.private.tracker
    movie_queue: yes
    template:
      - movies_imdb_filter
      - trakt_seen_movies

#searching for whatever is left in the movie_queue on a public tracker      
  torrentSearch:
    priority: 50
    torrent_alive: 10
    quality: 1080p
#need to add movie_queue to hava a plugin accepting stuff
    movie_queue: yes  
    discover:
      what:
        - emit_movie_queue: yes
      type: movies
      from:
        - torrentz: verified
#        - isohunt: movies
#        - piratebay: yes
#        - search_rss: http://torrentz.eu/feed_verifiedP?q={{search_term}}
#    delay: 24 hours
    template:
      - trakt_seen_movies

```
