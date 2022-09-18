---
title: torrent_size
description: 
published: true
date: 2022-09-18T05:14:45.066Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:14:42.511Z
---

# Torrent size
**Removed in r1202, replaced by [content_size](/Plugins/content_size)**

  
  
  

Reject torrents based on size. As this plugin only **Rejects**, you need to accept entries with some other filter (ie. [accept_all](/Plugins/accept_all), [series](/Plugins/series) etc.)

### Example:
```
torrent_size:
  min: 12
  max: 1200
```

Size is given in MB
