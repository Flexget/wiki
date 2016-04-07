= List Plugins =

List plugins are a special class of plugin, which work as input plugins, but can also be used in other contexts in order to edit the list.

||[wiki:Plugins/List/trakt_list trakt_list]||Use or add entries from one of your trakt.tv lists.||
||[wiki:Plugins/List/imdb_list imdb_list]||Use or add entries from one of your IMDB lists.||
||[wiki:Plugins/List/couchpotato_list couchpotato_list]||Use or add entries from one of your couchpotato watch list.||
||[wiki:Plugins/List/sonarr_list sonarr_list]||Use or add entries from Sonarr shows.||
||[wiki:Plugins/List/entry_list entry_list]||Use or add entries to a custom made entry list.||
||[wiki:Plugins/List/movie_list movie_list]||Use or add entries to a custom made movie list.||

=== Operating with lists ===

||[wiki:Plugins/List/list_add list_add]||Use this plugin to add accepted entries to another list plugin.||
||[wiki:Plugins/List/list_remove list_remove]||Use this plugin to remove accepted entries to another list plugin.||
||[wiki:Plugins/List/list_accept list_accept]||Use this plugin to accept entries based on another list plugin.||
||[wiki:Plugins/List/list_reject list_reject]||Use this plugin to reject entries based on another list plugin.||

== List action advanced usage ==
All of the aforementioned list plugins take a list of list plugin in their schema, so all operation can be used on multiple plugins at the same time:
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
  - imdb_list:
      login: email@123.com
      password: flexget
      list: watchlist
}}}