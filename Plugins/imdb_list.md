= IMDb list =

This plugin creates an [wiki:Entry Entry] for each movie in your IMDb list.

This plugin is useful for example when used in a feed with the [wiki:Plugins/queue_movies queue_movies] plugin to add movies from your IMDb watchlist to your [wiki:Plugins/movie_queue movie queue]

'''Example:'''

{{{
imdb_list:
  username: imdbusername
  password: mypassword
  list: watchlist
}}}

'''Note:''' Adding this to your movie feeds or preset will NOT cause movies in imdb's watchlist to be accepted since this is an input, not a filter.