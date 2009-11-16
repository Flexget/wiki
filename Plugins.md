= Plugins =

{{{
#!comment

# just ready for important info

#!html
#<h1 style="text-align: left; color: red">Note: Plugins page is being re-organized so many links are not working</h1>
#<b>This page contains plugins that are available only on bleeding edge.</b> 
}}}

0.9.x users should look [wiki:Modules here].


Plugins provide most of the functionality in !FlexGet. Plugins usually create, manipulate or download [wiki:Entry entries] but they can also change how !FlexGet operates.

Most plugins are enabled by placing a keyword and required settings in a configuration file.

== Indentation in examples ==

All configuration examples are assumed to be placed under a feed. So if documentation has example:

{{{
series:
  - name
}}}

In full configuration this goes into:

{{{
feeds:
  feed_name:
    rss: http://example.com
    series:
      - name
}}}

This makes examples more compact and reduces unnecessary boilerplate.

== Inputs ==

Produce [wiki:Entry entries] from external source.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/rss rss]||Parse RSS-feed.||
||[wiki:Plugins/html html]||Parse any HTML-page.||
||[wiki:Plugins/csv csv]||Parse any CSV-file||
||[wiki:Plugins/text text]||Parse any text data||
||[wiki:Plugins/listdir listdir]||'''{{{NEW}}}''' Use any local directory listing as a input.||
||[wiki:Plugins/rlslog rlslog]||Parse [http://rlslog.net] category.||
||[wiki:Plugins/scenereleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:Plugins/tvt tvt]||Parse [http://tvtorrents.com].||

== Filters ==

Reject or Accept [wiki:Entry entries] based on given rules. Single feed may have any number of filters.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/accept_all accept_all]||'''{{{NEW}}}'''  Accept all entries.||
||[wiki:Plugins/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugins/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugins/imdb_rated imdb_rated]||'''{{{NEW}}}''' Reject already voted entries.||
||[wiki:Plugins/imdb_queue imdb_queue]||'''{{{NEW}}}''' Accept movies from a predefined queue.||
||[wiki:Plugins/imdb_required imdb_required]||'''{{{NEW}}}''' Reject imdb incompatible entries.||
||[wiki:Plugins/series series]||'''{{{Upgraded}}}''' Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:Plugins/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugins/series_exists exists_series]||'''{{{New}}}''' Reject entries based on existing series in filesystem.||
||[wiki:Plugins/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugins/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugins/seen seen]||'''{{{Upgraded}}}''' Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugins/torrent_size torrent_size]||Reject torrents that do not meet size requirements.||
||[wiki:Plugins/nzb_size nzb_size]||Reject nzb's that do not meet size requirements.||

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand how filters co-operate.

== Outputs ==

Execute operation(s) to accepted entries.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/download download]||Download passed entries into given path.||
||[wiki:Plugins/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugins/statistics statistics]||Output statistics about downloaded entries.||
||[wiki:Plugins/subtitles subtitles]||Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:Plugins/exec exec]||Execute command for passed entries.||
||[wiki:Plugins/email email]||Send email when new content is passed.||
||[wiki:Plugins/deluge deluge]||'''{{{NEW}}}'''  Pass torrents directly to deluge bittorrent client.||
||[wiki:Plugins/sabnzbd sabnzbd]||'''{{{NEW}}}'''  Download nzbs with SABnzbd.||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/imdb_lookup imdb_lookup]||'''{{{NEW}}}'''  Tries to perform imdb lookup for all entries.||
||[wiki:Plugins/search search]||'''{{{NEW}}}'''  Search for download URL from supported sites.||
||[wiki:Plugins/path_by_ext path_by_ext]||'''{{{NEW}}}'''  Change (download) path based on file-type (extension).||
||[wiki:Plugins/preset preset]||'''{{{NEW}}}'''  Provides global configuration and named presets.||
||[wiki:Plugins/disable_plugin disable_plugin]||'''{{{NEW}}}'''  Disable plugins from presets.||
||[wiki:Plugins/cookies cookies]||'''{{{UPGRADED}}}''' Use !FireFox3 cookies.||
||[wiki:Plugins/interval interval]||Maintain minimum poll interval for a feed.||
||[wiki:Plugins/headers headers]||Modify HTTP headers.||
||[wiki:Plugins/extension extension]||Force a file extension.||
||[wiki:Plugins/regexp_resolve regexp_resolve]||Easy download URL rewriting.||
||[wiki:Plugins/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugins/cli_config cli_config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugins/try_regexp try_regexp]||Test how regexps work on feed(s) interactively.||
||[wiki:Plugins/disable_builtins disable_builtins]||Disable builtin modules from a feed.||
||[wiki:Plugins/formlogin formlogin]||'''{{{NEW}}}'''  Log in via form.||
||[wiki:Plugins/set set]||'''{{{NEW}}}'''  Set 'path' or other info per feed.||
||[wiki:Plugins/priority priority]||Change plugin priorities.||
||[wiki:Plugins/manipulate manipulate]||'''{{{NEW}}}'''  Allows regexp manipulation for entries.||
||[wiki:Plugins/sort sort]||'''{{{NEW}}}'''  Sort entries in a feed.||
||[wiki:Plugins/include include]||'''{{{NEW}}}'''  Include configuration from another yaml file.||
||[wiki:Plugins/delay delay]||'''{{{NEW}}}'''  Adds artificial delay into a feed.||
