## [CLI](/CLI) > `entry-list`
View and manage [entry lists](/Plugins/List/entry_list).

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `all`* || Shows all existing entry lists |
| `list`* || List entries from a list | 
|| *positional:* ||
|| `<list_name>` | Name of the list to display | 
| `show` || Show entry fields | 
|| *positional:* ||
|| `<list_name>` | Name of the list to display an entry from | 
|| `<entry>` | Entry title or ID from that list | 
| `add` || Add an entry to a list |
|| `list_name` | Name of the list to add to; if the list does not exist, it will be created | 
|| *positional:* ||
|| `<entry_title>` | Title of the entry | 
|| `<original_url>` | URL of the entry |
|| *optional:* ||
|| `--attributes <entry_field=value> [<entry_field=value> ...]` | Can be a string or a list of strings with the format imdb_id=XXX, tmdb_id=XXX, etc |
| `del` || Remove an entry from a list using its title or ID |
|| *positional:* ||
|| `<list_name>` | Name of the list to remove from | 
|| `<entry>` | Entry title or ID from that list | 
| `purge` || Removes an entire list with all of its entries; use this with caution |
|| *positional:* ||
|| `<list_name>` | Name of the list to remove |
|||<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||

### Examples
Note for all examples:
- The default `<list_name>` is `entries` for all CLI `entry-list` sub-commands.
- When prompted for an `<entry>`, it can be the entry ID displayed in `entry-list list <list_name>` or the exact title of the entry.

#### Return all entry lists names
```bash
$ flexget entry-list all
```

#### List all entries from an entry list
```bash
$ flexget entry-list list <list_name>
```

#### Show details about a specific entry
```bash
$ flexget entry-list show <list_name> <entry>
```

#### Add or update an entry on an entry list
Using a title and original URL is require. You can also add additional identifiers in the following format:

```bash
$ flexget entry-list add <list_name> <entry_title> <original_url> --attributes imdb_id=tt1234556 tmdb_id=1234
```

If the given entry list does not exist it will be created.

If the entry with the title exists on that list, its _entire_ list of attributes will be replaced by the given list of attributes (or removed altogether if such a list was not given). 

#### Removing an entry from an entry list
```bash
$ flexget entry-list del <list_name> <entry>
```

#### Clearing an entire entry list
```bash
$ flexget entry-list purge <list_name>
```