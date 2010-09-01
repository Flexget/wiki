= Entry =

Entry represent a single item created by input(s), usually a downloadable content.
It contains all the information necessary for [wiki:Plugins plugins] to perform their job.

For example [wiki:Plugins/regexp regexp] plugin checks if given regular expression matches entries '''title''' or '''url''' and acts accordingly.

'''Example of an entry:'''

These are mandatory fields

||'''Name'''||'''Value'''||
||title||Some.Awesome.Series.S01E01.XviD-Foo||
||url||!http://site.com/download/Some.Awesome.Series.S01E01.XviD-Foo.torrent||
||id||4be9694b5408e5d69a20ab2c0841edbf||

== Known fields ==

Entry ''may'' have any of these fields, but is not ''guaranteed'' to have any of them.

||'''Name'''||'''Created by'''||'''Description'''||
||path||||Path where this entry content should be saved||
||description||[wiki:Plugins/rss rss]||Item description||
||feed||metadata_feed||Feed name which this entry belongs to||
||quality||metadata_quality||Detected quality, ie. `720p`||
||series_name||[wiki:Plugins/series series]||Series name||
||series_season||[wiki:Plugins/series series]||Series season||
||series_episode||[wiki:Plugins/series series]||Series episode||
||series_id||[wiki:Plugins/series series]||Series episode identifier, ie. `S01E02` or `12.01.2009`||
||imdb_url||||Imdb url||
||imdb_id||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb identifier||
||imdb_name||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb name||
||imdb_year||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb year||
||imdb_score||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb score||
||imdb_votes||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb votes||
||imdb_genres||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb genres||
||imdb_languages||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb languages||
||imdb_photo||[wiki:Plugins/imdb_lookup imdb_lookup]*||Url for photo (hotlinking prevented)||
||imdb_plot_outline||[wiki:Plugins/imdb_lookup imdb_lookup]*||Plot outline||
||imdb_actors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Actors dictionary (key: imdbid, value: name)||
||imdb_directors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Actors dictionary (imdbid, name)||
||output||[wiki:Plugins/download download]||Downloaded file||
||torrent||modify_torrent||When entry is a torrent this contains [wiki:TorrentObject Torrent class]||
||data||[wiki:Plugins/download download]||Internal. Binary content.||
||content_size||[wiki:Plugins/content_size content_size]||Parsed size of torrents or NZBs.||
||location||[wiki:Plugins/listdir listdir]||The local filename of the entry.||

^* = and other plugins that utilize this plugin^

''More resources:''
 * [wiki:FilterOperations Actions for entry]