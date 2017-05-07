## [CLI](/CLI) > `failed`
list or clear remembered failures

### Sub-commands
| Sub-command | Description |
| --- | --- |
| `list`* | list all the entries that have had failures |
| `clear` | clear all failures from database, so they can be retried |
||<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> |

### Examples
```bash
#lists all the entries with failures
flexget failed list
```