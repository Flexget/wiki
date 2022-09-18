---
title: urlrewrite_newznab
description: 
published: true
date: 2022-09-18T05:25:06.944Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:16:23.630Z
---

# Newnzab plugin
The newznab plugin is used in conjunction with the [discover](/Plugins/discover) plugin.

With the [next_series_episodes](/Plugins/next_series_episodes)
```
discover:
  what:
    - next_series_episodes: yes
  from: 
    - newnab:
```

or the [movie_list](/Plugins/List/movie_list)

```
discover:
  what:
    - movie_list: movies
  from: 
    - newnab:
```


You need then to configure the newznab plugin, which take 4 parameters :
- website: website of the newznab server
- apikey:  most newznab require this key in order to execute a search on their website
- category: limit searches to this newznab category (tv, movie, or all)
- wait  interval between two newznab call: (default is 30 seconds)