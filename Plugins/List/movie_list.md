= Movie List =

This plugin is a [wiki:Plugins/List/ list_interface] plugin.

Stores a copy of an entry that was added to it if that entry contains the following attributes: `imdb_id`, `trakt_movie_id` or `tmdb_id`. This plugin replaces the now deprecated [wiki:Plugins/movie_queue movie_queue]. As opposed to [wiki:Plugins/movie_queue movie_queue], `movie_list` does not store quality or download status.

'''Note:''' When matching against `movie_list`, either with [wiki:Plugins/List/list_accept list_accept] or [wiki:Plugins/List/list_queue list_queue] the matched entries must have one of the aforementioned attributes, so consider using a lookup plugin like [wiki:Plugins/imdb_lookup imdb_lookup], [wiki:Plugins/trakt_lookup trakt_lookup] and etc. 

=== Schema ===

{{{
movie_list: <NAME>
}}}

=== Usage ===

As a [wiki:Plugins/List list_interface] plugin it follows the same list actions:

{{{
any_input: ...
filter: ...
list_add: 
  - movie_list: list name
}}}

It can be added as an additional output:

{{{
trakt_list:
  username: traktusername
  list: watchlist
  type: movies 
accept_all: yes
list_add:
  - movie_list: movies from trakt
}}}

This will add all accepted entries to an `movie_list` with the name `movies from trakt`. It then later be used as an input itself. This can be used a base to filter on with other tasks:

{{{
rss: ...
list_accept:
  - movie_list: movie from trakt
download: ...
}}}

You can create a list from multiple sources:

{{{
trakt_list:
  username: traktusername
  list: watchlist
  type: movies 
imdb_list:
  login: email@123.com
  password: flexget
  list: watchlist
list_add:
  - movie_list: all my watchlists
}}}

Example on how to migrate from [wiki:Plugins/movie_queue movie_queue]:

{{{
720p_movies_from_movie_queue:
  emit_movie_queue: yes
  accept_all: yes
  list_add:
    - movie_list: movies
  disable: 
    - seen # seen needs to be disabled since all the titles that movie queue will emit were seen when they were added to the queue
}}}

How to use it with a regular task:

{{{
a_task:
  rss: http://url.com/feed.xml
  quality: 720p # As opposed to movie_queue, movie_list does not hold quality attribute by itself, and needs to be added via the quality plugin if needed
  imdb_lookup: # movie-list requires entries with a recognizable attribute, as mentioned at the top
  list_queue:
    - movie_list: movie list name
  download: /path/to/download
}}}

How to use with discover plugin:
{{{
discover_task:
  discover:
    from:
      - movie_list: movie list name
    what:
     - kat: opts
  quality: 720p # As opposed to movie_queue, movie_list does not hold quality attribute by itself, and needs to be added via the quality plugin if needed
  imdb_lookup: # movie-list requires entries with a recognizable attribute, as mentioned at the top
  list_queue:
    - movie_list: movie list name
  download: /path/to/download
}}}

The [wiki:Plugins/List/list_queue list_queue] matches and immediately remove matching entity from list, so no duplicate matches will occur during a task. If you do no wish to remove on match, use [wiki:Plugins/List/list_accept list_accept] with `remove_on_accept` set to `False`.

== Movie list CLI ==

For detailed instruction about these CLI commands:
{{{
$ flexget movie-list -h
}}}


Movie list support CLI operations:

=== Return all movie lists names ===

{{{
$ flexget movie-list all
}}}

=== List movies from movie lists ===

{{{
$ flexget movie-list list -l <LIST_NAME>
}}}

=== Add or Update a movie to or from a movie list ===

Using a title is require. You can also add additional identifiers in the following format:

{{{
$ flexget movie-list add -l <LIST_NAME> -t <MOVIE_TITLE> -i imdb_id=tt1234556 tmdb_id=1234
}}}

Movie identifiers should correlate the list mentioned at the top, or they'll be ignored.

If a movie list does not exist it will be created.

If the movie with the title exists on that list, its list of identifiers will be replaced by given list of identifiers (or removed if such a list was not given).

=== Removing a movie from movie list ===

{{{
$ flexget movie-list del -l <LIST_NAME> -t <MOVIE_TITLE>
}}}

=== Clearing an entire movie list ===

{{{
$ flexget movie-list purge -l <LIST_NAME>
}}}


== Movie List API ==

`movie_list` plugin has full API support. See [http://discuss.flexget.com/t/flexget-rest-api/ API post] for details