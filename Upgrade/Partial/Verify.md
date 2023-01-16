---
title: Verify upgrade
description: 
published: true
date: 2023-01-16T20:04:10.784Z
tags: 
editor: markdown
dateCreated: 2023-01-16T19:57:17.927Z
---

## Verify

Check if your configuration file is still valid, there may have been some changes to the configuration format.

```cmd
flexget check
```

If your configuration doesn't pass check, have a look at [upgrade actions](/UpgradeActions) to see if there are any actions you must take. 

The behavior of certain plugins may also have changed, so checking [upgrade actions](/UpgradeActions) even if your config passes check is advisable.

For example, if you were running 3.1.2 follow all the steps above this revision.