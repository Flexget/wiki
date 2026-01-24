---
title: status
description: 
published: true
date: 2026-01-24T02:20:34.359Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:33.151Z
---

## [CLI](/CLI) > `status`*
View task health status.

### Optional arguments
| Argument | Description |
| --- | --- |
| `--task <task>` | Limit to results in specified `<task>` |
| `--limit <num>` | Limit to `<num>` results (default `50`) |

### Subcommands

| Command | Description |
| --- | --- |
| remove | Remove a task and all its execution records. Supports glob pattern matching.| 

### Examples
```bash
#shows the status for all tasks
$ flexget status

#displays status of the "foo_queue" task in porcelain table layout
$ flexget status --task "foo_queue" --porcelain
```