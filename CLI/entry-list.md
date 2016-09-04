## `entry-list`
view and manage entry lists

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
```bash
#shows all existing entry lists
flexget entry-list all
```

### Related articles
* [CUI / Command line interface overview](/CLI)