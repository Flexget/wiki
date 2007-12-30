= Input RlsLog =

Adds support for rlslog.net as a source.

If rlslog entry has NewTorrents download link then torrent url is parsed from there.
If rlslog entry has NewTorrents search link, we try to look from there if any of the results match entry title.
On multiple NewTorrents-links per entry have unknown effects ...

Module caches all successfull NewTorrents 'download torrent'-parses, hence module makes only one request per
rlslog-entry to NewTorrents thus eliminating any potential DDOS effect and or bandwith wasting.

Supports also piratebay links.

In case of movies the module supplies pre-parse IMDB-details (helps when chaining with [wiki:FilterImdb imdb] filter).