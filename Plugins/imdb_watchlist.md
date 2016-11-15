# IMDB watch list 

This plugin creates an [entry](/Entry) for each item in an IMDB list.

This plugin is useful for example when used in a task with the [wiki:Plugins/movie_queue movie_queue] plugin (in 'add' mode) to add movies from your IMDb watchlist to your movie queue.

**Notes:**

 * Like with other APIs used by !FlexGet the IMDb list is cached for 2 hours to avoid hammering.
 * List must be public.

## Example:

```yaml
imdb_watchlist:
  user_id: ur9999999
  list: watchlist
```

Your user id can be found [here](http://www.imdb.com/list/watchlist) when you are logged in.

*****WARNING:***** If you are using a list other than the `watchlist`, `ratings` or `checkins`, you currently have to look up the list id from imdb and use that instead of the name. 

**Note:** Adding this to your movie tasks or preset will NOT cause movies in IMDB's watchlist to be accepted since this is an input, not a filter.