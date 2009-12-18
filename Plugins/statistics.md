= Output Statistics =

'''UNMAINTAINED - WORKS POORLY'''


Output graphs about downloaded entries. The output is a single HTML file with graphs linked from Google chart API.

'''Example:'''

{{{
global:
   statistics: 
      file: ~/public_html/flexget_stats/index.html
}}}

= Output Statistics 2.0 =

The old statistics plugin is crap, no one maintains it, and it really doesn't log anything useful. Since !FlexGet 1.x has a fancy sqlite database, we can use that to get better statistics in addition to analyzing entries on output.

The next question is the drawing method, [http://code.google.com/apis/chart/ Google charts] (the current system) or [http://code.google.com/p/flot/ flot]?

== Database ==

=== What can we get? ===

* Number of episodes downloaded for each serie
* Quality for downloads (HDTV, 720p, etc..)
* Group names?

=== What do we WANT but can't? ===

* Download history for [wiki:Plugins/deluge] and [wiki:Plugins/transmissionrpc]

== Entries ==

=== What can we get? ===

* IMDB score (average score for downloaded movies?)
* Torrent size downloaded (min, max, average, average per feed)

=== What do we WANT but can't? ===
