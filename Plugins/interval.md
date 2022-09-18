---
title: interval
description: 
published: true
date: 2022-09-18T05:07:07.034Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:04.468Z
---

# Interval
Allows specifying minimum interval for task execution. If cron execution happens before interval is met the task is skipped.

Format: [n](/n) [minutes|hours|days|months](/minutes|hours|days|months)

Example:

```
interval: 7 days
```

**`NOTE:`** This is probably not useful in daemon mode. If you would like to set up the frequency of task execution in daemon mode, see [scheduling](/Daemon#scheduling).