= Input !RlsLog =

Adds support for [http://rlslog.net rlslog] as a source.

If rlslog entry has !NewTorrents or !PirateBay download link then torrent url is fetched from there. If !NewTorrents url points to search page 
we try to look if any of the results matches the title we are looking for.

Module caches all successful torrent url searches, so it only needs to perform lookup once from external site. This way module doesn't cause unnecessary load for those sites.

In case of movies the module supplies pre-parse IMDB-details (helps when chaining with [wiki:FilterImdb imdb filter]).

=== Problems ===

 * On multiple !NewTorrents links per entry have unknown effects.
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

This would download all dvdrips that have at least 6.1 score on imdb and at least 4500 votes. Movies with genres documentary or horror are rejected. See [wiki:FilterImdb imdb filter] for more information.