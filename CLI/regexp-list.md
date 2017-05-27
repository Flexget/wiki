---
import:
  - Includes/TableStylesDiv
---

## [CLI](/CLI) > `regexp-list`
View and manage [regexp lists](/Plugins/List/regexp_list).

### Sub-commands
| Sub-command | option | description |
| --- | --- | --- |
| `all`* || Shows all existing regexp lists |
| `list`* || List regexps from a list |
|| *positional:* ||
|| `<list_name>` | Name of the list to display | 
| `add` || Add a regexp to a list | 
|| `<list_name>` | Name of the list to add to | 
|| `<regexp>` | The regexp to add |
| `del` || Remove a regexp from a list | 
|| *positional:* ||
|| `<list_name>` | Name of the list to remove from | 
|| `<regexp>` | The regexp to remove |
| `purge` || Removes an entire list; use this with caution |
|| *positional:* ||
|| `<list_name>` | Name of the regexp list to remove |
{{> Includes/TableStylesDiv }}


### Examples
```bash
#lists all existing regexp lists
$ flexget regexp-list all
```