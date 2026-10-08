---
title: convert_magnet
description: 
published: true
date: 2026-10-08T13:26:44.898Z
tags: dependencies
editor: markdown
dateCreated: 2022-09-18T05:03:04.121Z
---

# Convert Magnet


> `libtorrent` is a required dependency.
{.is-warning}

Simple plugin for converting magnet links to torrent files without the use of torrent caches.

By default, the plugin will not fail entries if the conversion is unsuccessful, but setting `fail_entry_on_error: yes` will do so.

**Simple configuration**
```yaml
convert_magnet: yes|no
```

**With options**

```yaml
convert_magnet:
  timeout: n seconds|minutes
  fail_entry_on_error: yes|no
```