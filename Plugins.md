{{{
#!html
<h1 style="text-align: left; color: red">Note: Plugins page is being re-organized so many links are not working</h1>
<b>This page contains plugins that are available only on bleeding edge.</b> 
}}}
For older 0.9.x release, look instead [wiki:Modules here].

= Plugins =

Plugins provide most of the functionality in !FlexGet. Plugins usually create, manipulate or download [wiki:Entry entries] but they can as well change how !FlexGet operates.

Plugin is enabled by placing a keyword and required settings in a configuration file.

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
||[wiki:Plugin/rss rss]||Parse RSS-feed.||
||[wiki:Plugin/html html]||Parse any HTML-page.||
||[wiki:Plugin/csv csv]||Parse any CSV-file||
||[wiki:Plugin/text text]||Parse any text data||
||[wiki:Plugin/listdir listdir]||'''{{{NEW}}}''' Use any local directory listing as a input.||
||[wiki:Plugin/rlslog rlslog]||Parse [http://rlslog.net] category.||
||[wiki:Plugin/scenereleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:Plugin/tvt tvt]||Parse [http://tvtorrents.com].||

== Filters ==

Reject or Accept [wiki:Entry entries] based on given rules. Single feed may have any number of filters.

||'''Keyword'''||'''Description'''||
||[wiki:Plugin/accept_all accept_all]||'''{{{NEW}}}'''  Accept all entries.||
||[wiki:Plugin/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugin/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugin/imdb_rated imdb_rated]||'''{{{NEW}}}''' Reject already voted entries.||
||[wiki:Plugin/imdb_queue imdb_queue]||'''{{{NEW}}}''' Accept movies from a predefined queue.||
||[wiki:Plugin/imdb_required imdb_required]||'''{{{NEW}}}''' Reject imdb incompatible entries.||
||[wiki:Plugin/series series]||'''{{{Upgraded}}}''' Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:Plugin/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugin/series_exists exists_series]||'''{{{New}}}''' Reject entries based on existing series in filesystem.||
||[wiki:Plugin/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugin/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugin/seen seen]||'''{{{Upgraded}}}''' Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugin/torrent_size torrent_size]||Reject torrents that do not meet size requirements.||

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand how filters co-operate.

== Outputs ==

Execute operation(s) to accepted entries.

||'''Keyword'''||'''Description'''||
||[wiki:Plugin/download download]||Download passed entries into given path.||
||[wiki:Plugin/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugin/statistics statistics]||Output statistics about downloaded entries.||
||[wiki:Plugin/subtitles subtitles]||Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:Plugin/exec exec]||Execute command for passed entries.||
||[wiki:Plugin/email email]||Send email when new content is passed.||
||[wiki:Plugin/deluge deluge]||'''{{{NEW}}}'''  Pass torrents directly to deluge bittorrent client.||
||[wiki:Plugin/sabnzbd sabnzbd]||'''{{{NEW}}}'''  Download nzbs with SABnzbd.||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugin/imdb_lookup imdb_lookup]||'''{{{NEW}}}'''  Tries to perform imdb lookup for all entries.||
||[wiki:Plugin/search search]||'''{{{NEW}}}'''  Search for download URL from supported sites.||
||[wiki:Plugin/path_by_ext path_by_ext]||'''{{{NEW}}}'''  Change (download) path based on file-type (extension).||
||[wiki:Plugin/preset preset]||'''{{{NEW}}}'''  Provides global configuration and named presets.||
||[wiki:Plugin/cookies cookies]||'''{{{UPGRADED}}}''' Use !FireFox3 cookies.||
||[wiki:Plugin/interval interval]||Maintain minimum poll interval for a feed.||
||[wiki:Plugin/headers headers]||Modify HTTP headers.||
||[wiki:Plugin/extension extension]||Force a file extension.||
||[wiki:Plugin/regexp_resolve regexp_resolve]||Easy download URL rewriting.||
||[wiki:Plugin/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugin/cli_config cli_config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugin/try_regexp try_regexp]||Test how regexps work on feed(s) interactively.||
||[wiki:Plugin/disable_builtins disable_builtins]||Disable builtin modules from a feed.||
||[wiki:Plugin/formlogin formlogin]||'''{{{NEW}}}'''  Log in via form.||
||[wiki:Plugin/set set]||'''{{{NEW}}}'''  Set 'path' or other info per feed.||
||[wiki:Plugin/manipulate manipulate]||'''{{{NEW}}}'''  Allows regexp manipulation for entries.||
||[wiki:Plugin/sort sort]||'''{{{NEW}}}'''  Sort entries in a feed.||
||[wiki:Plugin/include include]||'''{{{NEW}}}'''  Include configuration from another yaml file.||
