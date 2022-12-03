---
title: convert_magnet
description: 
published: true
date: 2022-12-03T03:52:34.784Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:03:04.121Z
---

# Convert Magnet

Simple plugin for converting magnet links to torrent files without the use of torrent caches.

`libtorrent` is a required dependency. If you have Deluge installed, you'll also have libtorrent.

By default, the plugin will not fail entries if the conversion is unsuccessful, but setting `force: yes` will do so.

**Config**
```text
convert_magnet: yes|no
```
```text
convert_magnet:
  timeout: n seconds|minutes
  force: yes|no
```