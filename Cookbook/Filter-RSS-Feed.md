---
title: Filter-RSS-Feed
description: 
published: true
date: 2022-09-18T05:15:40.961Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:22.355Z
---

#  Filter RSS Feed to different folders
This setup will take a RSS Feed that you want to download everything from. For example, a RSS Feed of your torrent sites Bookmarks/Favorites/...  and will filter TV shows, Movies, and other (everything else) into separate locations. 
* Replace 'RSS Feed URL' with your Feeds URL 
* Change the downloader plugin (used here deluge) to your downloaders plugin, and change the set sections accordingly (may not be possible for all downloaders) 
* Change the folder locations from 'D:\...' to your setups. 
```
templates:
  book:
    rss: 
      url: '<RSS Feed URL>'
      all_entries: no
    # Replace with your Downloader plugin
    deluge:
      path: 'D:\Downloading'
      queuetotop: yes
    accept_all: yes
    no_entries_ok: yes
  
tasks:
  book-tv:
    priority: 1
    # Set your download location and label acording to downloader plugin
    set:
      movedone: 'D:\TV\{{ series_name }}'
      label: 'TV'
    exists_series: 'D:\TV\{{ series_name }}'
    metainfo_series: yes
    tvmaze_lookup: yes
    require_field:
      - tvmaze_series_name
    template: book

  book-movie:
    priority: 2
    # Set your download location and label acording to downloader plugin
    set:
      main_file_only:  yes
      keep_subs: yes
      hide_sparse_files: no
      movedone: 'D:\Movies'
      label: 'Movies'
    metainfo_movie: yes
    imdb_lookup: yes
    require_field:
      - imdb_name
    # For IMDB lookup issues failuers
    if:
      - imdb_name == None: reject
    template: book
      
  book-other:
    priority: 3
    metainfo_series: yes
    imdb_lookup: yes
    tvmaze_lookup: yes
    if:
      - has_field('imdb_name'): 
          # For IMDB lookup issues failuers
          if:
            - imdb_name != None: reject
      - has_field('tvmaze_series_name'): reject
    # Set your download location and label acording to downloader plugin
    set:
      movedone: 'D:\Other'
      label: 'Bookmarks'
    template: book
```
Uses plugins: [template](/Plugins/template), [priority](/Plugins/priority), [rss](/Plugins/rss), [deluge](/Plugins/deluge), [no_entries_ok](/Plugins/no_entries_ok), [set](/Plugins/set), [exists_series](/Plugins/exists_series), [tvmaze_lookup](/Plugins/tvmaze_lookup), [imdb_lookup](/Plugins/imdb_lookup), [accept_all](/Plugins/accept_all), [metainfo_series](/Plugins/metainfo_series), [require_field](/Plugins/require_field), [if](/Plugins/if), [metainfo_movie](/Plugins/metainfo_movie)


[Back to The Cookbook](/Cookbook)