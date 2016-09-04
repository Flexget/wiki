## `history`
View the history of entries that FlexGet has accepted

### Optional arguments
| argument | description |
| --- | --- |
| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
| `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain` |
| `--limit NUM` | limit to NUM results |
| `--search TERM` | Limit to results that contain TERM |
| `--task TASK` | Limit to results in specified TASK |
| `--short, -s` | Shorter output |


### Examples
```bash
#displays the accepted history in porcelain table format
flexget history --porcelain
```

### Related articles
* [CUI / Command line interface overview](/CLI)