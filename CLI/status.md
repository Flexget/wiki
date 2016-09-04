## `status`
View task health status

### Optional arguments
| argument | description |
| --- | --- |
| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
| `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain` |
| `--task TASK` | Limit to results in specified TASK |
| `--limit NUM` | Limit to NUM results |

### Examples
```bash
#shows the status for all tasks
flexget status
#displays status of the "foo_queue" task in porcelain table layout
flexget status --task "foo_queue" --porcelain
```

### Related articles
* [CUI / Command line interface overview](/CLI)