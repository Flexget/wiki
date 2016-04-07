= Movie List =

This plugin stores a copy of an entry that was added to it if that entry contains the following attributes: `imdb_id`, `trakt_movie_id` or `tmdb_id`.[[BR]] 
This plugin replaces the now deprecated [wiki:Plugins/movie_queue movie_queue]. As opposed to [wiki:Plugins/movie_queue movie_queue], `movie_list` does not store quality or download status.[[BR]]
This plugin is a [wiki:Plugins/List/ list_interface] plugin.
=== Schema ===
{{{
movie_list: <NAME>
}}}

=== Usage ===
As a [wiki:list_interface list_interface] plugin it follows the same list actions:
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
  quality: 720p
  list_add:
    - movie_list: 720p movies

1080p_movies_from_movie_queue:
  emit_movie_queue: yes
  quality: 1080p
  list_add:
    - movie_list: 1080p movies
}}}

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



