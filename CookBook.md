---
title: CookBook
description: 
published: true
date: 2022-09-18T04:49:02.096Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:48:59.487Z
---

templates:
  movie:
    transmission:
      host: localhost
      port: 9091
      username: tonychevalier
      password: Freezer*974
      addpaused: no
      path: /volume1/transmission/complete
    movie_queue: yes
    seen_movies: strict
    proper_movies: no
    
tasks:
  imdb-watchlist:
    imdb_list:
      username: tony@ton974.net
      password: Freezer*974
      list: watchlist
    accept_all: yes
    queue_movies:
      quality: dvdrip|bluray xvid|divx <720p
    priority: 2

  hd-watchlist:
    imdb_list:
      username: tony@ton974.net
      password: Freezer*974
      list: HDwatchlist
    accept_all: yes
    queue_movies:
      quality: dvdrip|bluray xvid|divx|h264 720p
    priority: 3

  ipt-movies:
    rss:
      url: https://www.oxtorrent.be/rss/films
      all_entries: no
    template: movie
    priority: 4