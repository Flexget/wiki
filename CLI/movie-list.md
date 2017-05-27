---
import:
  - Includes/TableStylesDiv
---

## [CLI](/CLI) > `movie-list`
View and manage [movie lists](/Plugins/List/movie_list).

### Sub-commands
| Sub-command | Option | Description |
| --- | --- | --- |
| `all`* || Shows all existing movie lists |
| `list`* || List movies from a list |
|| *positional:* ||
|| `<list_name>` | Name of the list to display | 
| `add` || Add a movie to a list | 
|| `<list_name>` | Name of the list to add to | 
|| *positional:* ||
|| `<movie_title>` | Title of the movie |
|| *optional:* ||  
|| `-i <identifiers> [<identifiers> ...]`, `--identifiers <identifiers> [<identifiers> ...]` | Can be a string or a list of string with the format `imdb_id=XXX`, `tmdb_id=XXX`, etc |
| `del` || Remove a movie from a list using its title | 
|| *positional:* ||
|| `<list_name>` | Name of the list to delete from | 
|| `<movie_title>` | Title of the movie | 
| `purge` || Removes an entire list with all of its movies; use this with caution |
|| *positional:* ||
|| `<list_name>` | Name of the list to remove |
{{> Includes/TableStylesDiv }}


### Examples
For detailed instruction about these CLI commands:

```cmd
$ flexget movie-list -h
```

Notes for all examples:
- If a list name isn't specified, the list name `movies` will be used by default. This is true for all actions.

#### Return all movie lists names
```cmd
$ flexget movie-list all
```

#### List movies from movie lists
```cmd
$ flexget movie-list list <list_name>
```

### Add or update a movie on a movie list
Using a title is required. You can also add additional identifiers in the following format:

```cmd
$ flexget movie-list add <list_name> <move_title> -i imdb_id=tt1234556 tmdb_id=1234
```

Movie identifiers should correlate to the list mentioned at the top, or they'll be ignored.

If the specified movie list does not exist, it will be created.

If the movie with the title exists on that list, its _entire_ list of identifiers will be replaced by the given list of identifiers (or removed altogether if such a list was not given).

Movies will be looked up from [IMDB](http://www.imdb.com) on add, with a fallback to [TMDB](http://www.tmdb.com). If both of these lookups fail, the movie will not be added to the list.

If a movie is added with identifiers, those will take precedence in the lookup before using its title.

#### Removing a movie from movie list
```bash
$ flexget movie-list del <list_name> <movie_title>
```

#### Clearing an entire movie list
```cmd
$ flexget movie-list purge <list_name>
```