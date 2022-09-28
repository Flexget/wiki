---
title: ConfigFileEditor-noarch-14spk
description: 
published: true
date: 2022-09-28T18:00:41.651Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:29:32.019Z
---

# Templates
  This is just in a template so that it can easily be re-used in multiple tasks (for example in an rss based and discover based task).
  If you only have one task using your series config, you can place   the `configure_series` plugin directly in that task rather than in a template.
  ```
  tv:
    configure_series:
      settings:
        # Configure all the series options to your taste
        quality: <=720p
        path: /volume1/TvShows/{{series_name}}/Season {{series_season}}/  # This will sort your downloads if you are using one of the output plugins which supports it
        identified_by: ep
      from:
        trakt_list:
          account: juricaz
          list: Watchlist
          type: shows
  ```
# Tasks
  This task will look for episodes you have added to your `Watchlist` list at trakt.
  It will set the `begin` series option for that show, then remove the episode and re-add it to your `Watchlist` list as a show.
  
```
  follow-from-trakt:
    seen: local
    trakt_list:
      account: juricaz
      list: Watchlist
      type: episodes
    accept_all: yes
    set_series_begin: yes
    list_remove:
      - trakt_list:
          account: juricaz
          list: Watchlist
          type: episodes
    list_add:
      - trakt_list:
          account: juricaz
          list: Watchlist
          type: shows
```
This task is what will actually download your shows.
See https://flexget.com/wiki/Cookbook/Series/Search for a more detailed explanation of how this search based task works, as well as an example of how to use your `tv` template on an rss-based task alongside.

```
discover-shows:
    # If this is your only task getting shows, you can just include 
    # the configure_series plugin here instead of using the template.
    template: tv
    discover:
      what:
        - next_series_episodes:
            from_start: yes
      from:
        - rarbg: 
              category:
                - x264 HDTV
        # Pick a search plugin(s) https://flexget.com/wiki/Searches
    # Add an appropriate output plugin here 
    # (perhaps `transmission` or `deluge` if you are using those clients.) 
    # https://flexget.com/wiki/Plugins#Output
    transmission:
      host: localhost
      port: 9091
      username: jurica
      password: bintaved26
  series:
    - Altered Carbon:
      begin: S03E01
    - Atlanta:
      begin: S03E01
    - Better Call Saul
      begin: S06E01
    - Black Mirror
      begin: S06E01
    - The Boys
      begin: S02E01
    - Dark
      begin: S03E01
    - The Expanse
      begin: S05E01
    - Glow
      begin: S04E01
    - The Handmaid's Tale
      begin: S04E01
    - Homecoming
      begin: S03E01
    - The Hook Up Plan
      begin: S03E01
    - It's Always Sunny in Philadelphia
      begin: S15E01
    - The Mandaloria
      begin: S02E01
    - Northern Exposure
      begin: S07E01
    - The Orville
      begin: S03E01
    - Red Dwarf
      begin: S13E01
    - Rick and Morty
      begin: S05E01
    - Russian Doll
      begin: S02E01
    - Search Party
      begin: S03E01
    - South Park
      begin: S24E01
    - Stranger Things
      begin: S04E01
    - The Toys That Made Us
      begin: S03E01
    - True Detective
      begin: S04E01
    - The Umbrella Academy
      begin: S03E01
    - Valley of the Boom
      begin: S02E01
    - The Venture Bros.
      begin: S08E01
    - Westworld
      begin: S04E01
    - The Witcher
      begin: S02E01
```

If you are using daemon mode, make sure you schedule the tasks in the right order, so that the begin episode gets set before it tries to download your shows
```
schedules:
  - tasks: [follow-from-trakt, discover-shows]
    interval:
      minutes: 30
```