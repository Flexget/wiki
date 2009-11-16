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
||series_name||[wiki:Plugins/series series]||Series name||
||series_season||[wiki:Plugins/series series]||Series season||
||series_episode||[wiki:Plugins/series series]||Series episode||
||series_id||[wiki:Plugins/series series]||Series identifier, ie. ''S01E02'' or ''12.01.2009''||
||imdb_score||[wiki:Plugins/imdb_lookup imdb_lookup]*||Retrieved/cached imdb score||
||output||[wiki:Plugins/download download]||Downloaded file||

^* = other plugins utilize this as well^

''More resources:''
 * [wiki:FilterOperations Actions for entry]
 * [wiki:DevelopersEntry Entry information for developers]