## `regexp-list`
View and manage regexp lists

### Actions
| actions | option | description |
| --- | --- | --- |
| `all`* || Shows all existing regexp lists |
| `list`* || List regexp from a list |
|| *positional:* ||
|| `list_name` | Name of the entry to operate on | 
| `add` || Add a regexp to a list | 
|| `list_name` | Name of the regexp list to operate on | 
|| `regexp` | The regexp |
| `del` || Remove a movie from a list using its title | 
|| *positional:* ||
|| `list_name` | Name of the movie list to operate on | 
|| `regexp` | The regexp |
| `purge` || Removes an entire list. Use this with caution |
|| *positional:* ||
|| `list_name` | Name of the movie list to operate on |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||


### Examples
```bash
#lists all existing regexp lists
flexget regexp-list all
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [regexp_list Plugin](/Plugins/List/regexp_list)