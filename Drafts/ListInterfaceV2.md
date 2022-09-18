---
title: ListInterfaceV2
description: 
published: true
date: 2022-09-18T04:58:09.705Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:07.119Z
---

# Refactor list usage
Just some ideas ...

Alternative to add_list, remove_list

```
manage_list:
  add:
    - movie_list: foobar
```

```
manage_list
  remove:
    - trakt_list:
        username: a_different_username
        list: watchlist
        type: movies
```


## list_accept, list_reject, list_queue mess
```
match_list:
  from:
    - [list](/list)
  [action](/action): [*accept*|reject](/*accept*|reject)
  [remove_on_match](/remove_on_match): [*yes*|no](/*yes*|no)
  [multiple_matches](/multiple_matches): [yes|*no*](/yes|*no*)
```

default marked with *

examples:

```
match_list:
  from:
    - trakt_list:
        username: traktusername
        list: watchlist
        type: movies
  action: accept
```
