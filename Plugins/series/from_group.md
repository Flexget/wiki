---
title: from_group
description: 
published: true
date: 2023-08-20T12:37:23.322Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:40.123Z
---

## Specify group (eg. anime fansubs)

**Example:**

```yaml
series:
  - some series name:
      from_group: fansubber 1
  - another series name:
      from_group:
        - fansubber 1
        - fansubber 2
```

**Supported notations:**

 * [Group] Series
 * Series XviD-Group

To disallow certain groups use [regexp](/Plugins/regexp) plugin to reject them.
