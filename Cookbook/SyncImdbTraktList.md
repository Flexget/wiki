---
title: SyncImdbTraktList
description: 
published: true
date: 2022-09-18T04:56:25.871Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:23.298Z
---

# Sync from an IMDb to a trakt.tv list
This recipe will keep your trakt watchlist in sync with your imdb watchlist. It is a one way sync, so direct changes to your trakt list will be overwritten by the imdb watchlist. This example is adaptable to sync any imdb list to any trakt list.

```
tasks:
  imdb_to_trakt:  # This task adds all the movies in your imdb watchlist to your trakt watchlist
    imdb_list:
      user_id: ur26726824
      list: watchlist
    accept_all: yes
    trakt_add:
      username: tom3297
      password: Atermial1!
      list: watchlist
    disable_builtins: [seen](/seen)  # If you wish to be able to remove things from the trakt list directly, without them being re-added, remove this line

  imdb_to_trakt_remove:  # This task removes anything in your trakt watchlist which is no longer in your imdb watchlist
    trakt_list:
      username: tom3297
      password: Atermial1!
      list: watchlist
      type: movies
    crossmatch:
      from:
        - imdb_list:
            user_id: ur26726824
            list: watchlist
      fields: [imdb_id](/imdb_id)
      action: reject
    accept_all: yes
    trakt_remove:
      username: tom3297
      password: Atermial1!
      list: watchlist
    disable_builtins: [seen](/seen)
```