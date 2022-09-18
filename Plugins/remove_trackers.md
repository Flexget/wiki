---
title: remove_trackers
description: 
published: true
date: 2022-09-18T05:10:57.190Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:54.645Z
---

# Remove Trackers
Removes trackers from torrent files using regexp matching. Also works on magnet urls.

### Example
```
remove_trackers:
  - moviex
```

This will remove all trackers that contain text moviex in their url.  
TIP: You can use [global preset](/Plugins/preset) in configuration to make this enabled on all tasks.