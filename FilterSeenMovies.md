= Filter Seen Movies =

Prevents movies being downloaded twice.
Works only on entries which have imdb url available. Meaning feed must have [wiki:FilterImdb imdb] module present or input needs to provide imdb urls (rare).

How duplicate movie detection works:
 * Remember all imdb urls from downloaded entries.
 * If stored imdb url appears again, entry is rejected.

== Configuration ==

There are two different operating modes, strict and loose.

Strict mode will remove all movies that are not imdb-compatible. Loose mode will pass them.

=== Example: ===

{{{
seen_movies: strict
}}}