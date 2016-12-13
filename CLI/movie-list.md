---
import:
  - TerminalTable
---

## `movie-list`
View and manage movie lists

### Actions
| actions | option | description |
| --- | --- | --- |
| `all`* || Shows all existing movie lists |
| `list`* || List movies from a list |
|| *positional:* ||
|| `<list name>` | Name of the entry to operate on | 
| `add` || Add a movie to a list | 
|| `list_name` | Name of the movie list to operate on | 
|| *positional:* ||
|| `movie_title` | Title of the movie |
|| *optional:* ||  
|| `-i <identifiers> [<identifiers> ...], --identifiers <identifiers> [<identifiers> ...]` | Can be a string or a list of string with the format `imdb_id=XXX`, `tmdb_id=XXX`, etc |
| `del` || Remove a movie from a list using its title | 
|| *positional:* ||
|| `list_name` | Name of the movie list to operate on | 
|| `movie_title` | Title of the movie | 
| `purge` || Removes an entire list with all of its movies. Use this with caution |
|| *positional:* ||
|| `list_name` | Name of the movie list to operate on |
|<div align="right">\* supports [table-styles](/CLI/--table-styles)</div> ||


### Examples
For detailed instruction about these CLI commands:

```cmd
$ flexget movie-list -h
```

Movie list support CLI operations:

### Return all movie lists names
```cmd
$ flexget movie-list all
```
{{>TerminalTable}}

### List movies from movie lists
```cmd
$ flexget movie-list list [LIST_NAME]
```

**Note:** If a list name isn't specified, list name `movies` will be used by default. This is true for all actions.
<br>{{>TerminalTable}}

### Add or Update a movie to or from a movie list
Using a title is require. You can also add additional identifiers in the following format:

```cmd
$ flexget movie-list add [LIST_NAME] <MOVIE_TITLE> -i imdb_id=tt1234556 tmdb_id=1234
```

Movie identifiers should correlate the list mentioned at the top, or they'll be ignored.

If the specified movie list does not exist it will be created.

If the movie with the title exists on that list, its list of identifiers will be replaced by given list of identifiers (or removed if such a list was not given).

Movies will be looked up from [IMDB](http://www.imdb.com) on add, with a fallback to [TMDB](http://www.tmdb.com). If both lookups fail, the movie will not be added to the list.

If a movie is added with identifiers, those will take precedence in the lookup before using its title.

### Removing a movie from movie list
```cmd
$ flexget movie-list del [LIST_NAME] <MOVIE_TITLE>
```

### Clearing an entire movie list
```cmd
$ flexget movie-list purge <LIST_NAME>
```



### Related articles
* [CUI / Command line interface overview](/CLI)
* [movie_list plugin](/Plugins/List/movie_list)