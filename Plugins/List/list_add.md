---
title: list_add
description: 
published: true
date: 2022-09-18T05:24:42.100Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:24:39.574Z
---

## List Add
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

List plugins can have entries added to them by using the `list_add` plugin:
```
trakt_list:
  username: traktusername
  list: watchlist
  type: movies
accept_all: yes
list_add:
  - trakt_list:
      username: a_different_username
      list: watchlist
      type: movies
```