---
title: quality
description: 
published: true
date: 2022-09-18T05:28:17.793Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:28:15.243Z
---

## Quality

| **Name** | **Description** |
| --- | --- |
| quality | Accept only qualities that match this quality requirement. No other quality will be accepted. |
| [qualities](/Plugins/series/qualities) | Accept all given qualities, multiple downloads |

Values should all be specified as a valid [quality requirement](/Qualities#Requirements) string.

**Example:**

```yaml
series:
  - name of series 1:
      quality: 720p+
  - name of series 2:
      quality: 1080p
  - name of series 3:
      quality: hdtv
```

Usually best way to specify quality for series is to use groups:

**Example:**

```yaml
series:
  720p:
    - name of series 1
    - name of series 2
  hdtv:
    - name of series 3
    - name of series 4
```

See [groups](/Plugins/series/per_group_settings) for more information.