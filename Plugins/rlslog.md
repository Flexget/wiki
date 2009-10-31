= Input !RlsLog =

Adds support for [http://rlslog.net rlslog] as a source.

=== Problems ===

 * Multiple torrent links per entry is untested.
 * If one rlslog entry contains multiple different entries (rarely).
 * Untested on other content besides movies.

== Example with imdb filtering: ==

{{{
rlslog: http://www.rlslog.net/category/movies/dvdrip/
imdb:
  min_score: 6.1
  min_votes: 4500
  reject_genres:
    - documentary
    - horror
download: ~/torrents
}}}

This would download all dvdrips that have at least 6.1 score on imdb and at least 4500 votes. Movies with genres documentary or horror are rejected. See [wiki:Plugin/imdb imdb filter] for more information.