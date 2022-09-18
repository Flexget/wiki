---
title: alternate_name
description: 
published: true
date: 2022-09-18T05:27:23.238Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:20.735Z
---

# Alternate Name
If a series is released under multiple names, you can use this option to define them. For example, original and translated name for a series.

Example:
```
series:
  - My Series:
      alternate_name: Meiner Serie
```

If more than one alternate name is needed, the option can be specified as a list:
```
series:
  - The Show:
      alternate_name:
        - De Show
        - Le Show
```