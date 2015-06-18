= Idea: add a new list interface plugins can follow. =
Used at task level, it would be an input plugin, and emit all items in its list. Same as something like trakt_list already does
In addition it would have methods to add and remove from the list. These could be called by another plugin, which allowed a list plugin to be nested inside.

== movie_queue reimplemented with a generic list backend ==
{{{
movie_queue:
  list:
    # Plugin implementing the list interface here
}}}
#e.g.
# db backed. Would be equivalent to current movie_queue
{{{
movie_queue:
  list:
    movie_list: myopts  # new plugin, like current movie_queue, but multiple named lists allowed and functionality other than add/delete/list movies in db removed
}}}
# online service backed
{{{
movie_queue:
  list:
    trakt_list: myopts  # same as current trakt list plugin, but with add/remove methods defined
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
(imdb_list couldn't implement the list interface though, since we can't programmatically add/remove.)

=== list_add/list_remove ===
output plugins to add/remove accepted entries from a list