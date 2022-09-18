---
title: TraktUpload
description: 
published: true
date: 2022-09-18T05:20:08.270Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:05.668Z
---

# Upload movie/tv collection to trakt.tv
These feeds will upload your collection to [trakt.tv](http://trakt.tv).

Upload movie collection to [trakt.tv](http://trakt.tv).
This is likely to generate errors and not work 100%. This is because of issues with other plugins. Most of my issues came from a unicode module not handling high order characters and the imdb plugin not matching all titles.

I would recommend making this a separate configuration file which you manually run only once or when needed. You can set up tract_acquired updating to your normal configuration file. If you put these into your config that is ran by cron, specify [interval](/Plugins/interval) for update feeds. Something along once per day or week.

```
tasks:

  Update-TV:
    filesystem:
      # Regex to match all video with these extensions in your collection
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
      path:
        # All the paths where you store TV episodes
        - /mnt/NMVideo/TV
        - /mnt/NMVideo/TV Anime
        - /mnt/NMVideo/TV Food
    metainfo_series: yes
    accept_all: yes
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey
      type: series

  Update-Movies:
    # For movies we use filesystem.
    filesystem:
      - /share/movies
    accept_all: yes
    imdb_lookup: yes
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey
      type: movies
```

Plugins used: [filesystem](/Plugins/filesystem), [accept_all](/Plugins/accept_all), [metainfo_series](/Plugins/metainfo_series), [imdb_lookup](/Plugins/imdb_lookup), [template](/Plugins/template), [trakt_acquired](/Plugins/trakt_acquired)
