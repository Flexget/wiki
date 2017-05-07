## [CLI](/CLI) > `history`
View the history of entries that FlexGet has accepted.

### Optional arguments
| Argument | Description |
| --- | --- |
| `--limit <num>` | Limit to `<num>` results |
| `--search <term>` | Limit to results that contain `<term>` |
| `--task <task>` | Limit to results in specified `<task>` |
| `--short`, `-s` | Shorter output |
||<div align="right">all support [table-styles](/CLI/--table-styles)|

### Examples
```bash
#displays the accepted history in porcelain table format
flexget history --porcelain
```