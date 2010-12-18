= Filter Seen Movies =

Prevents movies being downloaded twice.
Works only on entries which have imdb_url available, if imdb_url is already not present imdb lookup will be tried.

How duplicate movie detection works:
 * Remember all imdb urls from downloaded entries.
 * If stored imdb url appears again, entry is rejected.

== Configuration ==

There are two different operating modes, {{{strict}}} and {{{loose}}}.

Strict mode will reject all movies that are not imdb-compatible. Loose mode will not intervene them.

=== Example: ===

{{{
seen_movies: strict
}}}