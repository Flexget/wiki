---
title: Tommynator
description: 
published: true
date: 2022-09-18T05:22:43.290Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:40.616Z
---

This is my complete config.yml file. I will try to keep this up to date as much as possible.
My flexget version is 1.2.351

This config downloads all movies from my trakt watchlist, all new episodes from my trakt Following list, and sorts the series (movie sorting to be done) in the correct folder by season.
As soon as a movie or serie starts downloading I get a pushbullet notification, once a serie has been moved to the correct place, I also get a notification.

The RemoveEndedShows task is broken since end of June, since trakt_lookup uses old trakt api v1, which was closed on June 30th.

Things to be done: Simplify quality downloading (sort entries on quality instead of running 5 different tasks)
Sort movies with correct name
fix RemoveEndedShows
automatically move 1 new show from watchlist to following list every month

```
secrets: secrets.yml

templates:
  global:
    regexp:
      reject: 
        - SWESUB
        - FRENCH
        - RUS
        - trailer
        - SWE
        - SCREENER
        - CAM
  discoverMovies:
    movie_queue: accept
    tmdb_lookup: yes
    require_field:
      - tmdb_name
      - tmdb_year
    discover:
      what: 
        - emit_movie_queue: yes
      from:
        # - torrentz: verified
        - search_rss: http://torrentz.eu/feed?verified&q={{ search_term }}
      interval: 4 hours
    trakt_add:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: collection
    transmission:
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: /media/PlexMediaServer/Movies/
      magnetization_timeout: 30
      main_file_only: yes
      skip_files:
        - '*.nfo'
        - '*.sfv'
        - '*.[sS](/sS)ample'
        - '*.txt'
      include_subs: no
    pushbullet:
      apikey: '{{ secrets.pushbullet.APIkey }}'
      body: "{{ tmdb_name }} downloading with quality {{ quality }}"
      title: "Download started"
    trakt_remove:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: watchlist
  discoverSeries:
    configure_series:
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          password: '{{ secrets.trakt.password }}'
          list: Following
          type: shows
          strip_dates: yes
      settings:
        identified_by: ep
    exists_series:
      - /PlexMediaServer/Series
      - /PlexMediaServer/Downloading/Series
    discover:
      what:
        - emit_series:
            from_start: yes
      from:
        # - torrentz: verified
        - search_rss: http://torrentz.eu/feed?verified&q={{ search_term }}
      interval: 1 hours
    limit_new: 1
    thetvdb_lookup: yes
    require_field:
      - tvdb_series_name
      - series_season
      - series_episode
    transmission:
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: /PlexMediaServer/Downloading/Series/{{ tvdb_series_name }}/S{{ series_season|pad(2)}}E{{ series_episode|pad(2) }}
      magnetization_timeout: 30
      content_filename: "{{ tvdb_series_name }} - S{{ series_season|pad(2)}}E{{ series_episode|pad(2) }}"
      main_file_only: yes
      skip_files:
        - '*.nfo'
        - '*.sfv'
        - '*.[sS](/sS)ample'
        - '*.txt'
      include_subs: no
    pushbullet:
      apikey: '{{ secrets.pushbullet.APIkey }}'
      title: "Download started"
      body: "{{ tvdb_series_name }} - S{{ series_season|pad(2)}}E{{ series_episode|pad(2) }} downloading in {{ quality }}"
tasks:
  MovieQueue:
    priority: 1
    template: no_global
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: watchlist
      type: movies
    no_entries_ok: yes
    sort_by:
      reverse: yes
    exists_movie:
      path: /media/PlexMediaServer/Movies
      type: files
      #lookup: imdb
    limit_new: 1
    accept_all: yes
    movie_queue: add
  MoviesSearch1080pandhdtv:
    priority: 2
    template: discoverMovies
    quality: 1080p+ hdtv+
  MoviesSearch720pandhdtv:
    priority: 3
    template: discoverMovies
    quality: 720p+ hdtv+
  MoviesSearch720p:
    priority: 4
    template: discoverMovies
    quality: 720p+
  MoviesSearchhdtv:
    priority: 5
    template: discoverMovies
    quality: hdtv+
  MoviesSearchOther:
    priority: 6
    template: discoverMovies
    quality: 480p+
  ClearTransmission:
    no_entries_ok: yes
    clean_transmission:
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      transmission_seed_limits: yes
      enabled: yes 
  SeriesQueue:
    priority: 7
    trakt_emit:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: Following
      context: watched
      position: next
    accept_all: yes
    set_series_begin: yes
  SeriesSearch1080pandhdtv:
    priority: 8
    template: discoverSeries
    quality: 1080p+ hdtv+
  SeriesSearch720pandhdtv:
    priority: 9
    template: discoverSeries
    quality: 720p+ hdtv+
  SeriesSearch720p:
    priority: 10
    template: discoverSeries
    quality: 720p+
  SeriesSearchhdtv:
    priority: 11
    template: discoverSeries
    quality: hdtv+
  SeriesSearchOther:
    priority: 12
    template: discoverSeries
    quality: 480p+
  RemoveEndedShows:
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: Following
      type: shows
    trakt_lookup: yes
    if:
      - trakt_series_status == 'ended' or trakt_series_status == 'canceled': accept
    trakt_add:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: EndedShows
    pushbullet:
      apikey: '{{ secrets.pushbullet.APIkey }}'
      title: "Serie moved"
      body: "Serie {{ trakt_series_name }} was moved to EndedShows list because show status was {{ trakt_series_status }}"
    trakt_remove:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: Following
  Sort_Series:
    find: 
      path: /PlexMediaServer/Downloading/Series
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    disable: seen
    thetvdb_lookup: yes
    metainfo_series: yes
    require_field:
      - tvdb_series_name
      - series_season
      - series_episode
    accept_all: yes
    regexp:
      reject:
        - sample
    move:
      to: "/PlexMediaServer/Series/{{ tvdb_series_name }}/Season {{ series_season|pad(2) }}/"
      filename: '{{ tvdb_series_name }} - S{{ series_season|pad(2) }}E{{ series_episode|pad(2) }}'
      clean_source: 50
    pushbullet:
      apikey: '{{ secrets.pushbullet.APIkey }}'
      title: "Serie Sorted"
      body: "{{ tvdb_series_name }} - S{{ series_season|pad(2)}}E{{ series_episode|pad(2) }} was completed and moved into the correct folder." 
schedules:
  - tasks: [MovieQueue, MoviesSearch1080pandhdtv, MoviesSearch720pandhdtv, MoviesSearch720p, MoviesSearchhdtv, MoviesSearchOther]
    interval:
      hours: 4
  - tasks: [Sort_Series](/Sort_Series)
    interval:
      minutes: 15
  - tasks: [SeriesQueue, SeriesSearch1080pandhdtv, SeriesSearch720pandhdtv, SeriesSearch720p, SeriesSearchhdtv, SeriesSearchOther]
    interval:
      hours: 1
  - tasks: [ClearTransmission](/ClearTransmission)
    interval:
      days: 1
  - tasks: [RemoveEndedShows](/RemoveEndedShows)
    interval:
      weeks: 4
```