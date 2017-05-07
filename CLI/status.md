---
import:
  - TableStylesDiv
---

## [CLI](/CLI) > `status`*
View task health status.

### Optional arguments
| argument | description |
| --- | --- |
| `--task <task>` | Limit to results in specified `<task>` |
| `--limit <num>` | Limit to `<num>` results |
||{{> TableStylesDiv }}|
### Examples
```bash
#shows the status for all tasks
$ flexget status

#displays status of the "foo_queue" task in porcelain table layout
$ flexget status --task "foo_queue" --porcelain
```