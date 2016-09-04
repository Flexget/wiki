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
```bash
#lists all existing movie lists
flexget movie-list all
```

### Related articles
* [CUI / Command line interface overview](/CLI)
* [movie_list Plugin](Plugins/List/movie_list)