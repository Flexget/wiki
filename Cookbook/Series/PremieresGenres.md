---
title: PremieresGenres
description: 
published: true
date: 2022-09-18T05:20:50.685Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:48.146Z
---

# Premieres with genre filtering
```
tasks:
   get_shows:
      rss: https://www.xxxx.com/feeds.php?xxxx
      series_premiere: yes
      thetvdb_lookup: yes
      require_field: tvdb_genres
      regexp:
        reject:
          - documentary: {from: tvdb_genres}
          - talk show: {from: tvdb_genres}
          - game show: {from: tvdb_genres}
```

Adding this template to series feeds will download all premieres except if their genres are documentary, talk show or game show. This works only if the series data is already in the thetvdb when premiere is seen, not entirely sure if this is the case.

Uses plugins: [thetvdb_lookup](/Plugins/thetvdb_lookup), [require_field](/Plugins/require_field), [regepx](/Plugins/regexp),[series_premiere](/Plugins/series_premiere)
