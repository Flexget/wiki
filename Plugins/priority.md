---
title: priority
description: 
published: true
date: 2022-09-18T05:10:07.649Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:10:05.032Z
---

# Priority
This plugin changes task execution order. Without explicitly setting priority, tasks are executed in more or less random order. Execution order is 1,2,3...

**Example**

```
tasks:
  task a:
    priority: 10
  task b:
    priority: 20
  task c:
  task d: 
    priority: 5
```

In this example order is *task d, task a, task b,task c*.

You don't need to give priority to all tasks in your config. Just up the ones you wish to execute first.  Tasks with a priority value set will execute before those with no priority setting. You can even put multiple tasks with same priority number, in which case they will be executed with same priority but order is random within that priority.

