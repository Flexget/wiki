---
title: --tasks
description: 
published: true
date: 2024-10-21T06:28:46.072Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:01:01.695Z
---

# Command Line --tasks option
Allows running only selected tasks from the config.

**Syntax:**

```
--tasks <TASK> [TASK](/TASK)
```

where the given task names can also be glob patterns (i.e. using `*`, `?` or `[charsets](/charsets)`).


**Example:**

If you want to only execute a task called `mytask` run flexget like so:
```
flexget execute --tasks mytask
```

**Multiple tasks example:**

If you would like to run multiple tasks you can list them with comma separators (and no space.) This example runs `mytask` and `yourtask`:
```
flexget execute —-tasks mytask,yourtask
```

**Pattern example:**

If you would like to select a number of tasks that have similar names:
```
flexget execute --tasks "tv*"
```


**Grouping tasks by poll frequency:**

**NOTE** You can accomplish a similar effect with the [interval](/Plugins/interval) plugin, or using FlexGet's built-in scheduling in daemon mode. With this method you must be aware that two instances of FlexGet cannot run at the same time due to a lock file.

Another very useful application of the pattern selection is to have cron schedules like this:
```
*/5     * * * *         nice flexget execute --cron --tasks "*-5"
*/14    * * * *         nice flexget execute --cron --tasks "*-14"
```

You just need to append one of the supported poll intervals to your task names, and they'll get  automatically polled with that frequency. Note that the schedules are never triggered at the same minute, so they can never directly collide (if you have very slow tasks, some executions *might* be skipped due to the lock of a still running process).