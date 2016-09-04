## `rejected`
list or clear remembered rejections

### Actions
| action | option | description |
| --- | --- | --- |
| `list` || list all the entries that have been rejected |
|| `--table-type {plain,porcelain,github,single,double}` | Select output table style |
|| `--porcelain` | Make the output parseable. Similar to using `--table-type porcelain`
| `clear` || clear all rejected entries from database, so they can be retried |

### Examples
```bash
#lists all rejected entries
flexget rejected list
```

### Related articles
* [CUI / Command line interface overview](/CLI)