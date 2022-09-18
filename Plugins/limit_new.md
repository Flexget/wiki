---
title: limit_new
description: 
published: true
date: 2022-09-18T05:07:26.355Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:23.795Z
---

# Limit New
Limit number of new items.

Example:

```
limit_new: 1
```

This would allow only one new item to pass trough per execution.
Useful for passing torrents slowly into download, especially when adding new sources which would result massive concurrent downloads.

Note that since this is per execution, actual "flow rate" depends how often
FlexGet is executed.

Equivalent of poor mans queue for clients which do not support such feature.
