= Trakt list =

This plugin creates an [wiki:Entry Entry] for each movie/show in one of the available [http://trakt.tv trakt.tv] lists.

This plugin is useful for example when used in a feed with the [wiki:Plugins/queue_movies queue_movies] plugin to add movies from your trakt watchlist to your [wiki:Plugins/movie_queue movie queue], or to control the series plugin using [wiki:Plugins/import_series import_series].[[BR]]

'''Note:''' as with other APIs used by !FlexGet the trakt.tv list is cached for 2 hours to avoid hammering.

== Plugin Settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''username'''||This is your username at [http://trakt.tv trakt.tv] ||
||'''password'''||Your [http://trakt.tv trakt.tv] password. This is only required if your profile is protected, or to get private custom lists. ||
||'''api_key'''|| Your [http://trakt.tv trakt.tv] API key, this can be found at [http://trakt.tv/settings/api http://trakt.tv/settings/api] (if logged into trakt.tv) ||
||'''strip_dates'''||If set to {{{yes}}} the year will be removed from the end of titles that contain them.||
{{{#!td valign=top
'''movies'''
}}}
{{{#!td valign=top
Use a Movies category list as the input, options here are:
* all
* loved
* hated
* collection
* watchlist
}}}
|----------------
{{{#!td valign=top
'''series'''
}}}
{{{#!td valign=top
Use a Series category list as the input, options here are:
* all
* loved
* hated
* collection
* watchlist
* watched
}}}
|----------------
||'''custom'''|| Uses a custom list name as the input. (You must also specify password to retrieve private lists.) ||
}}}

== Config format ==

{{{
trakt_list:
  username: <trakt username>
  api_key: <api key>
  <media type>: <list type>
}}}

{{{trakt username}}} and {{{api key}}} should be filled in for your trakt account (your api key can be found [http://trakt.tv/settings/api here].) {{{media type}}} should be either 'series', 'movies' or 'custom'. {{{list type}}} can be one of the following for series and movies lists: 'all', 'collection', 'hated', 'loved', or 'watchlist'. For custom lists, {{{list_type}}} should be the name of the custom list.

'''Note:''' Adding this to your movie feeds or preset will NOT cause movies or series in the trakt list to be accepted since this is an input, not a filter.

=== Example ===

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

=== Example ===

This example shows how the trakt_list plugin could be used with the [wiki:Plugins/import_series import_series] plugin in order to download all of the series you have included in a custom trakt list called 'following shows'.
{{{
import_series:
  from:
    trakt_list:
      username: traktusername
      api_key: a098ae0eae09ae67ea
      custom: following shows
      strip_dates: yes
  settings:
    quality: 720p
}}}
