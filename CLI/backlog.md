## [CLI](/CLI) > `backlog`
View or clear entries from the [`backlog` plugin](/Plugins/backlog).
### Actions
| Argument | Option | Description |
| --- | --- | --- |
| `list`* || Show items in backlog |
||*positional:*|
| | `<task_name>`| Limit to items from specified `<task_name>`|
| `clear` || Clear all items in backlog |
|||<div align="right">* supports [table-styles](/CLI/--table-styles)</div>|

### Examples
```bash
#lists entries from the backlog of task "foo_task"
$ flexget backlog list foo_task

#lists entries from the backlog of task "foo_task" with porcelain table type
$ flexget backlog --porcelain list foo_task
```