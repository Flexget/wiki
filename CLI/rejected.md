---
import:
  - TableStylesDiv
---

## [CLI](/CLI) > `rejected`
List or clear [remembered rejections](/Plugins/remember_rejected).

### Sub-commands
| Sub-command | description |
| --- | --- |
| `list`* | List all entries that have been rejected |
| `clear` | Clear all rejected entries from the database so they can be retried |
||{{> TableStylesDiv }}|

### Examples
```bash
#lists all rejected entries
$ flexget rejected list
```