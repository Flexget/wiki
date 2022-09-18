---
title: torrent_alive
description: 
published: true
date: 2022-09-18T05:14:33.573Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:14:31.020Z
---

# Torrent Alive
This plugin will reject any accepted entries that are torrents, but do not meet a minimum seed requirement. Default is to require 1 seed.

Rejections are remembered by default for one hour. If the entry is accepted again after this interval, the tracker(s) will be queried for seeds again.

**`NOTE:`** This plugin only works if the tracker supports a standard scrape. It will cause entries to be rejected if none of the trackers for a torrent support scrape; In this case, do not use this plugin.

**Example:**
```
torrent_alive: yes
```

You can also specify the minimum number of seeds needed.
```
torrent_alive: 10
```

**Advanced Format:**

If you need to specify that rejections should last a different amount of time than 1 hour, you can use the advanced config format:
```
torrent_alive:
  min_seeds: 10
  reject_for: 15 minutes
```