= Entry =

Entry represent a single item created by input(s), usually a downloadable content.
It contains all the information necessary for [wiki:Plugins plugins] to perform their job.

For example [wiki:Plugins/regexp regexp] plugin checks if given regular expression matches entries '''title''' or '''url''' and acts accordingly.

'''Example of an entry:'''

||'''Name'''||'''Value'''||
||title||Some.Awesome.Series.S01E01.XviD-Foo||
||url||!http://site.com/download/Some.Awesome.Series.S01E01.XviD-Foo.torrent||

== Known fields ==

Entry ''may'' have any of these fields, but is not ''guaranteed'' to have any of them.

||'''Name'''||'''Created by'''||'''Description'''||
||path||||Path where this entry content should be saved||
||feed||metadata_feed||Feed name which this entry belongs to||
||quality||metadata_quality||Detected quality||
||series_name||[wiki:Plugins/series series]||Series name||
||series_season||[wiki:Plugins/series series]||Series season||
||series_episode||[wiki:Plugins/series series]||Series episode||
||series_id||[wiki:Plugins/series series]||Series episode identifier, ie. ''S01E02'' or ''12.01.2009''||
||imdb_url||||Retrieved/cached imdb score||
||imdb_score||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb score||
||imdb_votes||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb votes||
||imdb_year||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb year||
||imdb_genres||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb genres||
||imdb_languages||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb languages||
||output||[wiki:Plugins/download download]||Downloaded file||
||torrent||modify_torrent||When entry is a torrent this contains [wiki:TorrentObject Torrent class]||
||data||[wiki:Plugins/download download]||Internal. Binary content.||

^* = and other plugins that utilize this plugin^

''More resources:''
 * [wiki:FilterOperations Actions for entry]