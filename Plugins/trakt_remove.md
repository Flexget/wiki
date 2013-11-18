= Trakt Remove=
This plugin will remove movies in your [http://trakt.tv trakt.tv] list.

This plugin can be added to any of your tasks that download new movies, or it can be used with the [wiki:Plugins/listdir listdir] or [wiki:Plugins/find find] plugins to remove all your already acquired movies on trakt.tv from a specified list.

'''Configuration:'''

{{{
trakt_remove:
  username: <trakt username>
  password: <trakt password>
  api_key: <trakt api key>
  type: <movies>
  list: <trakt list name>
}}}
Your trakt api key can be found [http://trakt.tv/settings/api here].