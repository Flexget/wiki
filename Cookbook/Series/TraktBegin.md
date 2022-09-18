---
title: TraktBegin
description: 
published: true
date: 2022-09-18T05:27:32.249Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:41.802Z
---

# Sync series plugin begin episode with trakt
**`WARNING:`** This recipe may have issues until #2831 is fixed.

If you have a fresh FlexGet database, you might want to let it know where you are in all of your shows so that it doesn't start downloading episodes you already have/have seen. This recipe will set the [series begin](/Plugins/series/begin) episode based on your trakt database.

```
manual: yes  # You probably don't need to run this all the time, so you can launch it explicitly with the --tasks flag
trakt_emit:
  username: ***
  password: ***
  list: my list name
  context: watched  # You can set this to 'collected' depending on the state of your trakt info
  position: next
accept_all: yes
set_series_begin: yes
```