= IMDb list =

This plugin creates an [wiki:Entry Entry] for each item in an IMDb list.

This plugin is useful for example when used in a feed with the [wiki:Plugins/queue_movies queue_movies] plugin to add movies from your IMDb watchlist to your [wiki:Plugins/movie_queue movie queue]

'''Notes:''' 

 * Like with other APIs used by !FlexGet the IMDb list is cached for 2 hours to avoid hammering.

'''Example:'''

{{{
imdb_list:
  user_id: ur9999999
  list: watchlist
}}}

Your user id can be found [http://www.imdb.com/list/watchlist here] when you are logged in. (look in the url)

'''Example:'''

If your list is private, you will need to specify your imdb username and password. User_id is then not mandatory as plugin will figure it out for you.

{{{
imdb_list:
  list: watchlist
  username: me@somewhere.com
  password: mypassword
}}}

'''Note:''' Adding this to your movie feeds or preset will NOT cause movies in imdb's watchlist to be accepted since this is an input, not a filter.