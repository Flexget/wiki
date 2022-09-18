---
title: path
description: 
published: true
date: 2022-09-18T05:27:54.381Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:51.840Z
---

## Override path
Specify a custom path for a series. Note that this does **not** download it, your feed must have output plugin (eg. [download](/Plugins/download), [deluge](/Plugins/deluge))

**Example:**

```
series:
  - some series:
      path: ~/download/some_series/
  - another series
  - third series
download: ~/download/
```

Series `another series, third series` will be downloaded into `~/downloads`. However `some series` has overridden path and will be downloaded into `~/downloads/some_series/`.

It's also possible to set path globally from series name with [set](/Plugins/set) plugin, see [this recipe](/Cookbook/SetPath).