= Trakt Add =
This plugin will add accepted movies/tv episodes to one of your [http://trakt.tv trakt.tv] lists.

This plugin can be added to any of your tasks that deal with movies/series, or it can be used with the [wiki:Plugins/listdir listdir] or [wiki:Plugins/find find] plugins to add all your already acquired episodes/movies on trakt.tv to a specified list.

'''Configuration:'''

{{{
trakt_add:
  username: <trakt username>
  password: <trakt password>
  list: <list name>
}}}

The `list` option can be one of the built in trakt lists, `collection`, `watched`, or `watchlist`, or the name of one of your custom trakt lists.
