---
title: imdb_watchlist
description: 
published: true
date: 2022-11-13T04:25:06.962Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:06:41.768Z
---

# IMDB watch list 

This plugin creates an [entry](/Entry) for each item in an IMDB list.

This plugin is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin  to add movies from your IMDb watchlist to your movie list.

**Notes:**

 * Like with other APIs used by FlexGet the IMDb list is cached for 2 hours to avoid hammering.
 * List **must** be public.
 * Adding this to your movie tasks or preset will NOT cause movies in IMDB's watchlist to be accepted since this is an input, not a filter.
 * If you are using a list other than the `watchlist`, `ratings` or `checkins`, you currently have to look up the list id from imdb and use that instead of the name. 


## Example:

```yaml
tasks:
  populate_movie_list:
    imdb_watchlist:
      user_id: ur9999999
      list: watchlist
      force_language: es-mx # Optional - Force Specified Language
    accept_all: yes
    list_add:
      - movie_list: imdb_movies
```

Your user id can be found [here](http://www.imdb.com/list/watchlist) when you are logged in.<br>
You can force a returned language using the `force_language` parameter. A list of valid language values can be found [here](http://web.archive.org/web/20151206203420/http://www.science.co.il/Language/Locale-codes.asp). You will need to select the proper **LCID language string**.

