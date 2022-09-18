---
title: propers
description: 
published: true
date: 2022-09-18T05:28:10.033Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:28:07.497Z
---

## Propers
Default behavior is to download propers always.

To disable propers completely:

```
series:
  - some series:
      quality: 720p
      propers: no
```

To specify timeframe in which propers are accepted:

```
series:
  - some series:
      quality: 720p
      propers: 12 hours
```

Accepted format: NUM (minutes|hours|days|weeks)
