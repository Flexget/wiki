= Trakt Remove=
This plugin will remove movies, series or episodes from a [http://trakt.tv trakt.tv] list.

This plugin can be added to any of your tasks that deal with movies/series, or it can be used with the [wiki:Plugins/filesystem filesystem] plugin to remove all your already acquired movies on trakt.tv from a specified list.

'''Configuration:'''

{{{
trakt_remove:
  username: <trakt username>
  password: <trakt password>
  list: <list name>
}}}

The `list` option can be one of the built in trakt lists, `collection`, `watched`, or `watchlist`, or the name of one of your custom trakt lists.
