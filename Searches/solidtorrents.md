---
title: solidtorrents
description: 
published: true
date: 2024-06-02T03:39:28.026Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:47.774Z
---

# Solid Torrents
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

This search plugin will get results from [https://solidtorrents.net](/https://solidtorrents.net) or a reverse proxy if specified.

## Configuration
Simplest configuration, uses default search options. (all categories, sort by seeders)
```yaml
solidtorrents: yes
```
Advanced usage:

| Option | Description |
| --- | --- |
| category | One of: all, Audio, Video, Image, Document, eBook, Program, Android, Archive, Diskimage, Sourcecode, Database. Default is all. Keep in mind that it's case-sensitive. |
| sort_by | One of: seeders, leechers, downloads, date, size. Default is seeders. |
| sort_reverse | `yes` or `no`. |
| remove_potentially_unsafe | `yes` or `no`. Remove potentially unsafe torrents from result. Default is yes. |
| url | URL (including the protocol) used to access solidtorrents, i.e. to use a reverse proxy if the original domain is blocked. If not specified, the default used is `https://solidtorrents.net`
**Example:**
```yaml
solidtorrents:
  category: Video
  sort_by: leechers
  sort_reverse: no
  remove_potentially_unsafe: yes
  url: https://solidtorrents.net
```