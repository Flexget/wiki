---
title: from_group
description: 
published: true
date: 2022-09-18T05:27:42.658Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:40.123Z
---

## Specify group (eg. anime fansubs)
**Example:**

```
series:
  - fullmetal alchemist brotherhood:
      from_group: eclipse
  - naruto:
      from_group:
        - horriblesubs
        - crunchysubs
```

**Supported notations:**

 * [Group](/Group) Series
 * Series XviD-Group

To disallow certain groups use [regexp](/Plugins/regexp) plugin to reject them.
