---
title: add_trackers
description: 
published: true
date: 2022-09-18T05:10:05.024Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:43.780Z
---

# Add Trackers
Adds the listed trackers to any torrents grabbed by the feed. Also works on magnet urls.

### Example
```
add_trackers:
  - http://tracker1.com/announce
  - udp://tracker2.com/announce
```

TIP: You can use [global preset](/Plugins/preset) in configuration to make this enabled on all feeds.