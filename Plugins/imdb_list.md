= IMDb Watchlist =
This plugin creates an [wiki:Entry Entry] for each movie in your IMDb watchlist.

This plugin is most useful when used in a feed with the [wiki:Plugins/queue_movies queue_movies] plugin to add movies from your IMDb watchlist to your [wiki:Plugins/movie_queue movie queue]

'''Example:'''
{{{
  imdb_watchlist:
    username: imdbusername
    password: mypassword
}}}

'''Note:''' Adding this to your movie feeds or preset will NOT cause movies in imdb's watchlist to be accepted since this is an input, not a filter.