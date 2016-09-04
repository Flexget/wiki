## `backlog`
View or clear entries from backlog plugin
### Positional arguments
| argument | description |
| --- | --- |
| `{list,clear}` | Choose to show items in backlog, or clear all of them |
| `task` | Limit to specific task (if supplied) |
### Optional arguments
| argument | description |
| --- | --- |
| `-h, --help` | show this help message and exit |
| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
| `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain` |
### Examples
```bash
#lists entries from the backlog of task "foo_task"
flexget backlog list foo_task
#lists entries from the backlog of task "foo_task" with porcelain table type
flexget backlog --porcelain list foo_task
```
### Related articles
* [CUI / Command line interface overview](/CLI)