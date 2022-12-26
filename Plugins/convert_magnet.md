---
title: convert_magnet
description: 
published: true
date: 2022-12-05T03:23:32.800Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:03:04.121Z
---

# Convert Magnet


> `libtorrent` is a required dependency. If you have Deluge installed, you'll also have libtorrent.
{.is-warning}

Simple plugin for converting magnet links to torrent files without the use of torrent caches.

By default, the plugin will not fail entries if the conversion is unsuccessful, but setting `force: yes` will do so.

**Simple configuration**
```yaml
convert_magnet: yes|no
```

**With options**

```yaml
convert_magnet:
  timeout: n seconds|minutes
  force: yes|no
```