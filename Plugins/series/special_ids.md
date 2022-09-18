---
title: special_ids
description: 
published: true
date: 2022-09-18T05:28:33.445Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:28:30.884Z
---

# Special IDs

Define other terms on top of the default 'special' which will cause a release in this series to be flagged as a special.

Example:
```
series:
  - My Series:
      special_ids: short
```

If more than one is desired, the option can be specified as a list:
```
series:
  - The Show:
      special_ids:
        - short
        - OVA
```
