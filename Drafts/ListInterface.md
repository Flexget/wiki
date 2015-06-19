= Idea: add a new list interface plugins can follow. =
Used at task level, it would be an input plugin, and emit all items in its list. Same as something like trakt_list already does
In addition it would have methods to add and remove from the list. These could be called by another plugin, which allowed a list plugin to be nested inside.

== Plugins that could implement the list interface ==

  trakt_list:: Same as current trakt_list, but combine trakt_add/trakt_remove to fully implement list interface
  letterboxd_list:: Same as above
  entry_list:: New plugin, stores generic entries in db (I think this with the list_add, list_remove plugins below might replace digest plugin functionality as well)
  movie_list:: New plugin, stores movies in the database, perhaps a subclass of entry_list that enforces some extra rules regarding fields
  series_list:: New plugin, stores series in the database (also useful if you want to maintain series list for configure_series without depending on online service)

(imdb_list couldn't implement the list interface though, since we can't programmatically add/remove.)

== movie_queue reimplemented with a generic list backend ==
{{{
movie_queue:
  list:
    - # Plugin implementing the list interface here
}}}
#e.g.
# db backed. Would be equivalent to current movie_queue
{{{
movie_queue:
  list:
    - movie_list: myopts
}}}
# online service backed
{{{
movie_queue:
  list:
    - trakt_list: myopts
}}}
# This would be almost equivalent to this (already possible) config
{{{
crossmatch:
  from:
    - trakt_list: myopts
  fields:
    - imdb_id
    - tmdb_id
    - trakt_id
  action: accept
trakt_remove: myopts
}}}

== Other plugins to operate on generic lists ==
=== list_sync ===
Syncs a generic list plugin with all accepted entries
{{{
imdb_list: opts  # or 'listdir' might be another good one
accept_all: yes
list_sync:
 - trakt_list: opts
seen: no  # This would currently be required in any such task
}}}


=== list_add/list_remove ===
output plugins to add/remove accepted entries from a list

These replace current plugins like trakt_add/trakt_remove, but now you can use this for any of the list plugins, or multiple lists at once.

== interface plugins ==
=== webui ===
Webui plugins could be made which use these plugins as well, allowing nice interface to manage things like movie queues, series lists separate than
=== cli ===
Ideally every list plugin wouldn't have to write their own cli interface. Not exactly sure how this would be implemented though, as where would you write the config for the different list pluigns.