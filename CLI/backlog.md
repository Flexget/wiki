## [CLI](/CLI) > `backlog`
View or clear entries from the [`backlog` plugin](/Plugins/backlog).
### Actions
| Argument | Description |
| --- | --- |
| `{list,clear}`* | Choose to show items in backlog or clear all of them |
| `task`* | Limit to specific task (if supplied) |
||<div align="right">* supports [table-styles](/CLI/--table-styles)</div>|

### Examples
```bash
#lists entries from the backlog of task "foo_task"
flexget backlog list foo_task
#lists entries from the backlog of task "foo_task" with porcelain table type
flexget backlog --porcelain list foo_task
```