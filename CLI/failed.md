---
import:
  - Includes/TableStylesDiv
---

## [CLI](/CLI) > `failed`
list or clear remembered failures

### Sub-commands
| Sub-command | Description |
| --- | --- |
| `list`* | List all the entries that have had failures |
| `clear` | Clear all failures from database so they can be retried |
{{> Includes/TableStylesDiv }}

### Examples
```bash
#lists all the entries with failures
$ flexget failed list
```