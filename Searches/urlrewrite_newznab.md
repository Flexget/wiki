---
title: urlrewrite_newznab
description: 
published: true
date: 2022-09-18T05:25:06.944Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:11.047Z
---

# Newznab plugin
The newznab plugins is used in conjunction with the [discover](/Plugins/discover) plugins.

With the [next_series_episodes](/Plugins/next_series_episodes)
```
discover:
  what:
    - next_series_episodes: yes
  from: 
    - newznab:
        website: <value>
        apikey: <value>
        category: <value>
```

or the [movie_list](/Plugins/List/movie_list)

```
discover:
  what:
    - movie_list: movies
  from: 
    - newznab:
        website: <value>
        apikey: <value>
        category: <value>
```


You need then to configure the newznab plugins, which take 3 parameters:


| **Option** | **Description** |
| --- | --- |
| website | website of the newznab server |
| apikey | most newznab requires this key in order to make search on their website |
| category | type of search to do on newznab tv or movie |
