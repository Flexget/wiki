---
title: reorder_quality
description: 
published: true
date: 2022-09-18T05:11:01.052Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:58.401Z
---

# Reorder Quality

This plugin allows you to reorder the built-in [qualities](../Qualities) in a simple fashion. Qualities can only be reordered within the same quality type eg. a codec cannot be above a resolution.

### Config
```text
  reorder_quality:
    <name>:
      above|below: <another name>
```

### Example
This example will prefer webrip over hdtv.
```yaml
  download-task:
    rss: ...
    series:
      - WebRipRules
    reorder_quality:
      webrip:
        above: hdtv
```