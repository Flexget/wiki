---
title: execute
description: 
published: true
date: 2022-09-19T00:19:06.127Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:53:42.902Z
---

## [CLI](/CLI) > `execute`
Execute tasks now. If FlexGet is not running as a [daemon](/Daemon) or via [cron](/InstallWizard/Partial/Crontab), this is the only way tasks can be executed.

### Arguments
[Execute Arguments](/ExecuteArguments){.include}

### Examples
```bash
#executes the "foo_task"
$ flexget execute --tasks foo_task
```