= Trakt list =

This plugin creates an [wiki:Entry Entry] for each movie/show in one of the available [http://trakt.tv trakt.tv] lists.

This plugin is useful for example when used in a feed with the [wiki:Plugins/queue_movies queue_movies] plugin to add movies from your trakt watchlist to your [wiki:Plugins/movie_queue movie queue][[BR]]
Please note that as with other APIs used by flexget the trakt.tv list is cached for 6 hours to avoid hammering.

'''Config format:'''

{{{
trakt_list:
  username: <trakt username>
  api_key: <api key>
  <media type>: <list type>
}}}

{{{trakt username}}} and {{{api key}}} should be filled in for your trakt account (your api key can be found [http://trakt.tv/settings/api here].) {{{media type}}} should be either 'series' or 'movies'. {{{list type}}} can be one of the following: 'all', 'collection', 'hated', 'loved', or 'watchlist'.

'''Example:'''

This example shows how you would use trakt_list plugin with [wiki:Plugins/queue_movies queue_movies], in order to add all the movies from your trakt watchlist to your [wiki:Plugins/movie_queue movie queue]. This example should be in its own feed, not combined with your movie downloading feed.

{{{
trakt_list:
  username: traktusername
  api_key: a098ae0eae09ae67ea
  movies: watchlist
accept_all: yes
queue_movies:
  quality: 720p bluray
}}}

'''Example:'''

This example shows how the trakt_list plugin could be used with the [wiki:Plugins/import_series import_series] plugin in order to download all of the series you have marked as loved on trakt.
{{{
import_series:
  from:
    trakt_list:
      username: traktusername
      api_key: a098ae0eae09ae67ea
      series: loved
  settings:
    quality: 720p
}}}

'''Note:''' Adding this to your movie feeds or preset will NOT cause movies in the trakt list to be accepted since this is an input, not a filter.