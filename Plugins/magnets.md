---
title: magnets
description: 
published: true
date: 2022-09-18T05:14:38.606Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:42.673Z
---

# Magnets
This plugin will remove any magnet links from the entry urls list, and reject any entries that only have magnet links. 

Since [torrent_cache](/Plugins/torrent_cache) is a built-in plugin, this will mean that most entries fall back to a torrent cache link rather than being rejected. 

This is useful if you are using the [download](/Plugins/download) plugin as output, or if you are using the 
[content_filter](/Plugins/content_filter) or [content_size](/Plugins/content_size) plugins, which cannot get the required information from magnets.

### Usage
```
magnets: no
``` 