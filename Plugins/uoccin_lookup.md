---
title: uoccin_lookup
description: 
published: true
date: 2022-09-18T05:16:02.900Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:00.283Z
---

# Uoccin Lookup
This plugin looks up for the information stored in the local uoccin.json file about any entries that FlexGet has identified as movies or series. uoccin_lookup will populate more entry fields that can be used in other plugins.


| uoccin_collected | The movie or the episode is marked as collected |
| --- | --- |
| uoccin_rating | The movie or series assigned rating (as set in the [Uoccin](https://play.google.com/store/apps/details?id=net.ggelardi.uoccin) Android app, if used) |
| uoccin_subtitles | The movie or episode downloaded subtitles |
| uoccin_tags | The movie or series assigned tags (by [uoccin_watchlist_add](/uoccin_watchlist_add) plugin, or in the app) |
| uoccin_watched | The movie or the episode is marked as watched |
| uoccin_watchlist | The movie or series is in the watchlist |

**`IMPORTANT:`** The plugin requires on the entries the **imdb_id** field to identify the movies, or the **tvdb_id** field to identify the series, so it is usually necessary to use it in combination with [imdb_lookup](/imdb_lookup) or [thetvdb_lookup](/thetvdb_lookup).

## Plugin Settings
The plugin requires the path to the uoccin.json file.

**Examples:**

This plugin can be used in combination with the [if](/if) plugin to filter the entries:

```
purge_movies:
    imdb_lookup: yes
    uoccin_lookup: path_to_uoccin_folder
    filesystem:
      path:
        - C:\Storage\Videos\Incoming\movies
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    if:
      - uoccin_watched and uoccin_rating <= 4: accept
    delete:
      clean_source: 50
```

```
get_premieres:
    thetvdb_lookup: yes
    uoccin_lookup: path_to_uoccin_folder
    inputs:
      - rss: some_rss_feed
    series_premiere: yes
    if:
      - uoccin_tags or uoccin_watchlist or uoccin_watched or uoccin_collected: reject
    transmission:
      bandwidthpriority: -1
```