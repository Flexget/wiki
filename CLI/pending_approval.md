---
title: pending_approval
description: 
published: true
date: 2022-09-18T05:09:41.566Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:54:09.833Z
---

## [CLI](/CLI) > `pending`
View and manage entries [pending approval](/Plugins/pending_approval).

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `list`* | List pending entries |
|| *optional:* ||
|| `--task-name <task_name>` | Filter by `<task_name>` |
|| `--approved` | Show only approved entires|
|| `--pending` | Show only pending entires|
| `approve` || Approve pending entries |
|| *positional:* ||
|| `(<entry_id>|all)` | Approve one pending entry by ID, or all pending entries |
| `reject` || Reject pending entries |
|| *positional:* ||
|| `(<entry_id>|all)` | Reject one pending entry by ID, or all pending entries |
| `clear` | Clear all unapproved pending entries |
|| *optional:* ||
|| `--task-name <task_name>` | Filter by task name ||
{{> Includes/TableStylesDiv }}

### Examples
```bash
# List all pending entries
$ flexget pending list

# Approve all pending entries
$ flexget pending approve all
```