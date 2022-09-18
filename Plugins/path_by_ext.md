---
title: path_by_ext
description: 
published: true
date: 2022-09-18T05:09:25.220Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:22.655Z
---

# Path by ext
Allows overwriting entry path based on it's extension / mime-type.

### Example (extension)
These work only if python is aware of related mime-types.

```
path_by_ext:
  torrent: ~/watch/torrent/
  nzb: ~/watch/nzb/
```

### Example (mime-type)
This works always when server sends correct mime-type. A bit harder to use tough.

```
path_by_ext:
  "application/x-bittorrent": ~/watch/torrent/
  "application/x-nzb": ~/watch/nzb/
```