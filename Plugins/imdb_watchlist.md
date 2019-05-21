# IMDB watch list 

This _input_ plugin creates an [entry](/Entry) for each item in an IMDB list. This item is not downloadable.

This is useful for example when used in a task with the [movie_list](/Plugins/List/movie_list) plugin to add movies from your IMDb watchlist to your movie list(s).

**Notes:**

 * Like with other APIs used by FlexGet the IMDb list is cached for 2 hours to avoid hammering.
 * List **must** be public.
 * All IMDb lists are **read only**. FlexGet cannot modify them in any way.
 * If you are using a list other than the `watchlist`, `ratings` or `checkins`, you currently have to look up the list id from imdb and use that instead of the name. 
  * You can force a returned language using the `force_language` parameter. A list of valid language values can be found [here](http://www.science.co.il/Language/Locale-codes.asp). You will need to select the proper **LCID language string**.

Your user id can be found [here](http://www.imdb.com/list/watchlist) when you are logged in.<br>

## CLI
Various commandline tools are available, please refer to:

```bash
$ flexget movie-list -h
```

### Example:

Task which takes imdb watchlist and syncs it into FlexGet [movie_list](/Plugins/List/movie_list) and name the list _movies_.

```yaml
populate_movie_list:
  imdb_watchlist:
    user_id: ur9999999
    list: watchlist
    force_language: es-mx # Optional - Force Specified Language
  accept_all: yes
  list_add:
    - movie_list: movies
```

To see what are in the movie list, run

```bash
$ flexget movie-list list
```

Another task is needed to actually download movies from previously synced  [movie_list](/Plugins/List/movie_list).

```yaml
download_movies:
  rss: http://example.com/feed.xml
  list_match:
    from:
      - movie_list: movies
  download: ~/watchdir/
```