---
title: content_size
description: 
published: true
date: 2023-07-29T17:16:50.645Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:03:00.354Z
---

# Content size
Allow specifying minimum and maximum sizes for contents such as torrents and nzbs. By default the plugin operates in "strict" mode where if the size of a download cannot be determined it will be rejected.

**Note:** content_size doesn't work with magnet links, as it works by analyzing the the .torrent file. You can include the [magnets](/Plugins/magnets) plugin to reject any magnet entries.

### Example:
```
content_size:
  min: 12 MiB
  max: 1 GiB
  strict: no
```

Size can be given with a unit (B KB, MB, GB, PB.) To use binary units rather than decimal ones, use the appropriate abbeviation (B, KiB, MiB, GiB, TiB.) If size is given without a unit, it is assumed to be in Mebibytes.

This would reject all torrents below 12 MiB and above 1 GiB and over rides the strict behaviour. Same would work also for nzbs. As this plugin only **rejects**, you need to accept entries with some other filter (ie. [accept_all](/Plugins/accept_all), [series](/Plugins/series) etc.)