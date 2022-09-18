---
title: only_new
description: 
published: true
date: 2022-09-18T05:10:54.634Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:15.024Z
---

# Only New
Process only new entries.

**NOTE:** This plugin is not needed on tasks just using the rss plugin as input. The rss plugin has (more efficient) built-in functionality that makes this plugin redundant.

All undecided entries are rejected at the end of the task execution and will be rejected by the [remember_rejected](/Plugins/remember_rejected) plugin on all future executions of the task.

This should not be needed on most tasks, and may cause problems in instances where processing an entry on the second run is desired (e.g. lookup was not available first run.) It is most helpful in cases where performance is an issue.

**Example:**

```
only_new: yes
```

You can allow old entries to be viewed and processed again by running the `flexget rejected` command. In addition, rejections will be automatically forgotten if the configuration for the task has changed since the last run.