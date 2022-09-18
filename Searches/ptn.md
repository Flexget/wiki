---
title: ptn
description: 
published: true
date: 2022-09-18T05:18:31.117Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:28.546Z
---

# PtN
This plugin searches the private bittorent site PtN. You'll need to enter your username, password, as well as your login key, which can be found on your profile page.

**Basic config:**
```
ptn:
  username: xxxx
  password: xxxx
  login_key: xxxx
```

**Configuring categories:**

By default, the results will include torrents from all categories, however you can also list out the categories you want it to search. Valid categories are:
- 1080p
- 720p
- bdrip
- bluray
- brrip
- dvdr
- dvdrip
- mp4
- ost/flac
- ost/mp3
- packs
- !r5/scr
- remux
- tvrip
- webrip

This goes into the config like:
```
ptn:
  username: xxxx
  password: xxxx
  login_key: xxxx
  categories:
    - 720p
    - bluray
    - 1080p
```