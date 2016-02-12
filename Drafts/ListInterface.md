= Idea: add a new list interface plugins can follow. =
Used at task level, it would be an input plugin, and emit all items in its list. Same as something like trakt_list already does
In addition it would have methods to add and remove from the list. These could be called by another plugin, which allowed a list plugin to be nested inside.

Alternative implementation idea: Rather than implement the different list methods on the plugin itself, have one method which, returns an object following the `collections.MutableSet` interface. (prototype [https://github.com/Flexget/Flexget/commit/0d0d1165bd0575c2ad5431905eee21887a6f891d here])

== Plugins that could implement the list interface ==

  trakt_list:: Same as current trakt_list, but combine trakt_add/trakt_remove to fully implement list interface
  letterboxd_list:: Same as above
  entry_list:: New plugin, stores generic entries in db (I think this with the list_add, list_remove plugins below might replace digest plugin functionality as well)
  movie_list:: New plugin, stores movies in the database, perhaps a subclass of entry_list that enforces some extra rules regarding fields
  series_list:: New plugin, stores series in the database (also useful if you want to maintain series list for configure_series without depending on online service) (maybe entry_list is good enough for this?)
  regex_list:: New plugin, determines matches based on field regexes. Could be used in list_queue to work like regexp plugin, but for things you just want to get once.

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

=== alternate movie queue reimplementation ===
Rather than have the movie matching logic in the `movie_queue` plugin, make a generic `queue` plugin, and have the list interface define the matches. We then make a movie_list plugin with the list interface, and the contains method on that list will do the movie matching logic (marking a match if any of the known movie ids match.) 
{{{
queue:
  list:
    - movie_list: options
}}}
The idea here is that we could then make e.g. a `regex_list` plugin, which could define its `contains` method rules to return true if the regex of the list item matches given entry.

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

Example task, do something with items in a trakt list then remove them:
{{{
trakt_list: myopts
accept_all: yes
# Do something here
list_remove:
  - trakt_list: myopts
}}}

== interface plugins ==
=== api ===
Allows a single api endpoint to be written which will support viewing/editing any list plugins.
=== webui ===
Webui plugins could be made which use these plugins as well, allowing nice interface to manage things like movie queues, series lists separate than
=== cli ===
Ideally every list plugin wouldn't have to write their own cli interface. Not exactly sure how this would be implemented though, as where would you write the config for the different list pluigns.