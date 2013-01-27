= Trakt Acquired =
This plugin will mark accepted movies/tv episodes in your [http://trakt.tv trakt.tv] library.

This plugin can be added to any of your tasks that download new tv/movies, or it can be used with the [wiki:Plugins/listdir listdir] or [wiki:Plugins/find find] plugins to [wiki:Cookbook/Movies/TraktUpload mark all your already acquired shows on trakt.tv].

'''Configuration:'''

{{{
trakt_acquired:
  username: <trakt username>
  password: <trakt password>
  api_key: <trakt api key>
  type: <movies|series>
}}}
Your trakt api key can be found [http://trakt.tv/settings/api here].