= Trakt list =

'''IMPORTANT: Please see [wiki:Plugins/trakt trakt] on how to authorize Flexget to access your private Trakt.tv account.'''

This plugin creates an [wiki:Entry Entry] for each movie/show in one of the available [http://trakt.tv trakt.tv] lists.

This plugin is useful for example when used in a task with the [wiki:Plugins/movie_queue movie_queue] plugin to add movies from your trakt watchlist to your [wiki:Plugins/movie_queue movie queue], or to control the series plugin using [wiki:Plugins/configure_series configure_series].[[BR]]

This plugin is a [wiki:list_interface list_interface] plugin.

'''Notes:''' 

 * Like with other APIs used by !FlexGet the trakt.tv list is cached for 2 hours to avoid hammering.
 * Adding this plugin to your movie tasks or preset will NOT cause movies or series in the trakt list to be accepted since this is an input, not a filter.
 * If your trakt lists are not publicly available, you will need to authorize your account via the `flexget trakt auth` CLI command, then specify the '''account''' in your trakt configuration. 
 * IMPORTANT: [http://support.trakt.tv/knowledgebase/articles/154739-why-do-things-get-removed-from-my-watchlist-after- Trakt removes shows from watchlist if you watch them, so DO NOT use watchlist as your primary series source, use a custom list instead!]
 * If you want HTML-formatted lists, ex: "<b>TV Shows:</b> Get", to use that list, enter the list on trakt.tv and copy the part of the url that mentions it (ex: "b-tv-shows-b-get"). Basically, the displayed list name is '''not''' the same as the URL-friendly name, and trakt_list wants the URL-friendly name!

== Plugin Settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''username'''||This is the username at [http://trakt.tv trakt.tv] which owns the list. If `account` is specified, this will default to the owner of said account.||
||'''account'''||This is only required if the profile is protected, or to get private custom lists. It should be created via the `flexget trakt auth` CLI command.||
||'''strip_dates'''||If set to {{{yes}}} the year will be removed from the end of titles that contain them.||
||'''list'''||Name of a custom trakt list, or one of the built in ones: `watchlist`, `collection`, or `watched`
||'''type'''||Type of items to be listed, can be one of: `movies`, `shows`, or `episodes`

== Config format ==

{{{
trakt_list:
  username: <trakt username>
  account: <account set up in CLI> (this is required if the list is not publicly available)
  list: <list name>
  type: <movies|shows|episodes>
}}}

=== Example: Queue movies ===

This example shows how you would use trakt_list plugin with [wiki:Plugins/movie_queue movie_queue], in order to add all the movies from your trakt watchlist to your [wiki:Plugins/movie_queue movie queue]. This example should be in its own task, not combined with your movie downloading task.

{{{
trakt_list:
  username: traktusername
  account: traktusername # required if list is not public
  list: watchlist
  type: movies
accept_all: yes
movie_queue: add
}}}

=== Example: Autoconfigure series ===

This example shows how the trakt_list plugin could be used with the [wiki:Plugins/configure_series configure_series] plugin in order to download all of the series you have included in a custom trakt list called 'following shows'.

{{{
configure_series:
  from:
    trakt_list:
      username: traktusername
      account: traktusername # required if list is not public
      list: following shows
      type: shows
  settings:
    quality: 720p
}}}

=== List action example ===
{{{
trakt_list:
  username: traktusername
  list: watchlist
  type: movies
accept_all: yes
list_add:
  - trakt_list:
      username: a_different_username
      list: watchlist
      type: movies
}}}
For more information about list action go to the [wiki:list_interface list_interface] page.