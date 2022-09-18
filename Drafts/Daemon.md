---
title: Daemon
description: 
published: true
date: 2022-09-18T04:57:46.719Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:44.113Z
---

# Daemon / Scheduler
Implement daemon mode + scheduler.

**Configuration draft**:

```
schedule:
  default:
    .
    .
  feed_name:
    .
    .
  another_feed:
    .
    .
```

Note, it should be possible to define interval as minutes, hours, days and ideally all these either per day or every day.

**Draft 1:**

```
schedule:
  default:
    *: 1 hours      # default interval for all days (* may not be valid key?)
  some_feed:
    tue: 10 minutes # overrides tuesday from default
    wed: None       # no scheduling for wednesday
```

Daemon / schedule mode trough --daemon parameter (status | start | stop | reload).

**Draft 2:**

```
schedule:
  default:
    interval: 30m # 30 minute interval as default
  some_feed:
    interval: 24h # once per day for this one
  some_other_feed:
    interval: 30s # and once every 30 seconds (or less if the run takes over 30s to complete)
```