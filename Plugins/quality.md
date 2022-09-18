---
title: quality
description: 
published: true
date: 2022-09-18T05:12:42.022Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:28.137Z
---

# Quality

Allows specifying acceptable qualities. All other qualities will be rejected. 

**NOTE:** If you are using another plugin with it's own quality detection, i.e. [series](/Plugins/series), it might offer more functionality. Additionally mixing series quality options and quality plugin will cause weird behavior.

## Simple Usage

With the simple usage, you just specify which quality you want.

```
quality: 720p+ hdtv
```

Any valid [quality requirements](/Plugins/quality#qualities) string can be used here.

You can also use a list form to specify multiple quality requirement strings that are acceptable. In this case, only entries that do not match at least one of the quality strings will be rejected.

```
quality:
  - 720p hdtv
  - 1080p webdl
```

{{> Qualities }}
