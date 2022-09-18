---
title: piratebay
description: 
published: true
date: 2022-09-18T05:18:27.276Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:24.726Z
---

# Pirate Bay
This search plugin will get results from [https://thepiratebay.org](/https://thepiratebay.org) or a reverse proxy if specified.

## Configuration
Simplest configuration, uses default search options. (all categories, sort by seeders)
```
piratebay: yes
```
Advanced usage:

| Option | Description |
| --- | --- |
| category | One of: all, audio, music, video, tv, movies, highres movies, highres tv, comics. You can also directly specify the category number from thepiratebay if the category you need is not directly supported. |
| sort_by | One of: date, size, seeds, leechers, default (note that this is the piratebay default search order, flexget sorts by seeds by default) |
| sort_reverse | `yes` or `no`. |
| url | URL (including the protocol) used to access the piratebay, i.e. to use a reverse proxy if the original domain is blocked. If not specified, the default used is `https://thepiratebay.org`
**Example:**
```yaml
piratebay:
  category: video
  sort_by: leechers
  url: https://piratebaymirror.eu
```