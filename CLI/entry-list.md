---
import:
  - TerminalTable
---

## `entry-list`

View and manage entry lists

### Actions
| argument | option | description |
| --- | --- | --- |
| `all`* || Shows all existing entry lists |
| `list`* || List entries from a list | 
|| *positional:* ||
|| `<list name>` | Name of the list to operate on | 
| `show` || Show entry fields. | 
|| *positional:* ||
|| `list_name` | Name of the list to operate on | 
|| `entry` | Can be entry title or ID | 
| `add` || Add an entry to a list |
|| `list_name` | Name of the list to operate on | 
|| *positional:* ||
|| `entry_title` | Title of the entry | 
|| `original_url` | URL of the entry |
|| *optional:* ||
|| `--attributes <attributes> [<attributes> ...]` | Can be a string or a list of string with the format imdb_id=XXX, tmdb_id=XXX, etc |
| `del` || Remove an entry from a list using its title or ID |
|| *positional:* ||
|| `list_name` | Name of the list to operate on | 
|| `entry` | Can be entry title or ID | 
| `purge` || Removes an entire list with all of its entries. Use this with caution |
|| *positional:* ||
|| `list_name` | Name of the list to operate on |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||

### Examples

Entry list support CLI operations:

### Return all entry lists names
```bash
$ flexget entry-list all
```

### List entry from entrylists
```bash
$ flexget entry-list list <LIST_NAME>
```
Default <LIST_NAME> is `entries`. This is true for all CLI actions.
<br>{{> TerminalTable }}
### Show details about a specific entry
```bash
$ flexget entry-list show <LIST_NAME> <ENTRY>
```

`<ENTRY>` can be the ID displayed in `entry-list list` or exact entry title.
<br>{{> TerminalTable }}

### Add or Update a entry to or from an entry list
Using a title and original URL is require. You can also add additional identifiers in the following format:

```bash
$ flexget entry-list add <LIST_NAME> <ENTRY_TITLE> <ORIGINAL_URL> --attributes imdb_id=tt1234556 tmdb_id=1234
```

If the given entry list does not exist it will be created.

If the entry with the title exists on that list, its list of attributes will be replaced by given list of attributes (or removed if such a list was not given).

### Removing an entry from entry list
```bash
$ flexget entry-list del <LIST_NAME> <ENTRY>
```
`<ENTRY>` can be the ID displayed in `entry-list list` or exact entry title.

### Clearing an entire entry list
```bash
$ flexget entry-list purge <LIST_NAME>
```

### Related articles
* [CUI / Command line interface overview](/CLI)