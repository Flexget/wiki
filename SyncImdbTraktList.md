---
title: SyncImdbTraktList
description: 
published: true
date: 2022-09-18T04:51:49.449Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:46.867Z
---

tasks:
  imdb_to_trakt:  # This task adds all the movies in your imdb watchlist to your trakt watchlist
    imdb_list:
      user_id: urXXXXXXXX
      list: watchlist
    accept_all: yes
    trakt_add:
      username: myusername
      password: mypassword
      list: watchlist
    disable_builtins: [seen](/seen)  # If you wish to be able to remove things from the trakt list directly, without them being re-added, remove this line

  imdb_to_trakt_remove:  # This task removes anything in your trakt watchlist which is no longer in your imdb watchlist
    trakt_list:
      username: myusername
      password: mypassword
      list: watchlist
      type: movies
    crossmatch:
      from:
        - imdb_list:
            user_id: urXXXXXXXX
            list: watchlist
      fields: [imdb_id](/imdb_id)
      action: reject
    accept_all: yes
    trakt_remove:
      username: myusername
      password: mypassword
      list: watchlist
    disable_builtins: [seen](/seen)