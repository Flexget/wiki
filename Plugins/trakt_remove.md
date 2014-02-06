= Trakt Remove=
This plugin will remove movies, series or episodes from a [http://trakt.tv trakt.tv] list.

This plugin can be added to any of your tasks that deal with movies/series, or it can be used with the [wiki:Plugins/listdir listdir] or [wiki:Plugins/find find] plugins to remove all your already acquired movies on trakt.tv from a specified list.

'''Configuration:'''

{{{
trakt_remove:
  username: <trakt username>
  password: <trakt password>
  api_key: <trakt api key>
  list: <list name>
}}}

The `list` option can be one of the built in trakt lists, `library`, `seen`, or `watchlist`, or the name of one of your custom trakt lists.

Your trakt api key can be found [http://trakt.tv/settings/api here].