= Entry =

Entry represents one item provided by input module, a downloadable content. 
It contains all the information necessary for modules to perform their job.

For example [wiki:FilterPatterns patterns] module checks if given regular
expression matches entry title or url and if not item is filtered.

See [wiki:modules] for more information how entries are used.

== Information for developers ==

Entry is actually just a dictionary.

Mandatory attributes:

{{{
title          : name of the entry
url            : url where content can be found
}}}

Optional common attributes (3rd party modules may use more):

{{{
imdb_url       : Points to imdb-movie-page (string)
imdb_score     : Pre-parsed score/rating value (float)
imdb_votes     : Pre-parsed number of votes (int)
imdb_year      : Pre-parsed production year (int)
imdb_genres    : Pre-parsed genrelist (array)
imdb_languages : Pre-parsed languagelist (array)
torrent        : If entry is torrent this contains [wiki:TorrentObject Torrent class] in some module roles.
path           : Path where this entry should be saved.
}}}