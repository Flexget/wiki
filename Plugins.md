= Plugins =

{{{
#!comment

# just ready for important info

#!html
#<h1 style="text-align: left; color: red">Note: Plugins page is being re-organized so many links are not working</h1>
#<b>This page contains plugins that are available only on bleeding edge.</b> 
}}}

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

Produce [wiki:Entry entries] from external source.[[BR]]
Most requests are cached so there is no penalty for example using same RSS URL multiple times in the configuration.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/apple_trailers apple_trailers]||Get movie trailers from Apple.com||
||[wiki:Plugins/csv csv]||Parse any CSV-file||
||[wiki:Plugins/find find]||'''{{{NEW}}}''' Search through a local directory looking for files as a input.||
||[wiki:Plugins/html html]||Parse any HTML-page.||
||[wiki:Plugins/input_imdb_queue imdb_queue_input]||'''{{{NEW}}}''' Get entries from IMDB queue to pass to search plugin||
||[wiki:Plugins/listdir listdir]||'''{{{NEW}}}''' Use any local directory listing as a input.||
||[wiki:Plugins/rlslog rlslog]||Parse [http://rlslog.net] category.||
||[wiki:Plugins/rss rss]||Parse RSS-feed.||
||[wiki:Plugins/scenereleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:Plugins/tail tail]||Tail a log file (eg. irc logs)||
||[wiki:Plugins/text text]||Parse any text data||
||[wiki:Plugins/tvt tvt]||'''BROKEN''' Parse [http://tvtorrents.com].||

== Filters ==

Reject or Accept [wiki:Entry entries] based on given rules. A single feed may have any number of filters.[[BR]]
If you plan to use multiple filters per feed, you should look at [wiki:Filtering filtering operations] to understand how they work.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/accept_all accept_all]||Accept all entries.||
||[wiki:Plugins/all_series all_series]||'''{{{NEW}}}'''  Accepts any entry that appears to be an episode of a series.||
||[wiki:Plugins/content_filter content_filter]||'''{{{NEW}}}'''  Reject based on filenames within torrents.||
||[wiki:Plugins/content_size content_size]||'''{{{NEW}}}'''  Reject torrents and nzb's that do not meet size requirements.||
||[wiki:Plugins/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugins/exists_series exists_series]||Reject entries based on existing series in filesystem.||
||[wiki:Plugins/exists_movie exists_movie]||Reject entries based on existing movies in filesystem.||
||[wiki:Plugins/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugins/imdb_rated imdb_rated]||Reject movies you've already voted on imdb.||
||[wiki:Plugins/imdb_required imdb_required]||Reject imdb incompatible entries.||
||[wiki:Plugins/imdb_queue imdb_queue]||Accept movies from imdb queue.||
||[wiki:Plugins/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugins/only_new only_new]||'''{{{NEW}}}'''  Causes all entries that were in the feed on the previous run to be rejected at the input phase.||
||[wiki:Plugins/private_torrents private_torrents]||'''{{{NEW}}}'''  Reject private or public torrents.||
||[wiki:Plugins/quality quality]||'''{{{NEW}}}'''  Reject entries not of the specified quality.||
||[wiki:Plugins/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugins/require_field require_field]||'''{{{NEW}}}'''  Reject entries that do not have the specified fields.||
||[wiki:Plugins/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugins/seen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugins/series series]||Accept TV-series episodes. Quality and episode number aware.||
||[wiki:Plugins/series_premiere series_premiere]||'''{{{NEW}}}'''  Accept any entry that appears to be the first episode of a series.||

== Configuration ==

These plugins configure other plugins from external sources like 3rd party sites.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/thetvdb_favorites thetvdb_favorites]||'''{{{NEW}}}'''  Configures the series plugin with all the shows you have marked as favorites at http://thetvdb.com.||
||[wiki:Plugins/import_series import_series]||'''{{{NEW}}}'''  Configures the series plugin with all the shows given by any input plugin (eg. listdir, rss). ||

== Outputs ==

Execute operation(s) on accepted entries.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/deluge deluge]||Pass torrents directly to deluge bittorrent client.||
||[wiki:Plugins/download download]||Download passed entries into given path.||
||[wiki:Plugins/email email]||Send email when new content is passed.||
||[wiki:Plugins/exec exec]||'''{{{UPGRADED}}}'''  Executes commands on entries.||
||[wiki:Plugins/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugins/prowl prowl]||Send prowl notifications (iPhone).||
||[wiki:Plugins/sabnzbd sabnzbd]||Download nzbs with SABnzbd.||
||[wiki:Plugins/subtitles subtitles]||UNFINISHED. Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:Plugins/transmission transmission]||Pass entries' url to transmission, supporting magnet links.||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/add_trackers add_trackers]||'''{{{NEW}}}'''  Add trackers to torrents.||
||[wiki:Plugins/archive archive]||'''{{{NEW}}}'''  Archive all seen entries for searchable database for later retrieval.||
||[wiki:Plugins/cookies cookies]||'''{{{UPGRADED}}}'''  Use FireFox3 cookies.||
||[wiki:Plugins/delay delay]||Adds artificial delay into a feed.||
||[wiki:Plugins/disable_builtins disable_builtins]||Disable builtin plugin(s) from a feed.||
||[wiki:Plugins/disable_plugin disable_plugin]||'''{{{NEW}}}''' Disable plugins from presets.||
||[wiki:Plugins/extension extension]||Force a file extension.||
||[wiki:Plugins/formlogin formlogin]||Log in via form.||
||[wiki:Plugins/free_space free_space]||'''{{{NEW}}}''' Abort feed when drive space is low.||
||[wiki:Plugins/headers headers]||Modify HTTP headers.||
||[wiki:Plugins/include include]||Include configuration from another yaml file.||
||[wiki:Plugins/imdb_lookup imdb_lookup]||Tries to perform imdb lookup for all entries.||
||[wiki:Plugins/interval interval]||Maintain minimum poll interval for a feed.||
||[wiki:Plugins/manipulate manipulate]||'''{{{NEW}}}''' Allows regexp manipulation for entries.||
||[wiki:Plugins/manual manual]||'''{{{NEW}}}''' Only run the a feed when explicitly specified.||
||[wiki:Plugins/path_by_ext path_by_ext]||Change (download) path based on file-type (extension).||
||[wiki:Plugins/priority priority]||Change feed execution order.||
||[wiki:Plugins/plugin_priority plugin_priority]||Change plugin priorities.||
||[wiki:Plugins/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugins/preset preset]||Provides global configuration and named presets.||
||[wiki:Plugins/search search]||Search for download URL from supported sites.||
||[wiki:Plugins/set set]||'''{{{UPGRADED}}}'''  Set 'path' or other info per feed. Can be dynamic per entry.||
||[wiki:Plugins/sort_by sort_by]||Sort entries in a feed.||
||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Fetch series information from thetvdb.||
||[wiki:Plugins/urlrewrite urlrewrite]||User regexp for URL Rewriting.||

== Metainfo ==

These are usually automatic ([wiki:Builtin]) plugins which provide metainfo (fields) to [wiki:Entry].

||[wiki:Plugins/metainfo_quality metainfo_quality]||Parses quality from the entry.||
||[wiki:Plugins/metainfo_feed metainfo_feed]||Populates feed field for entries.||
||[wiki:Plugins/metainfo_series metainfo_series]^1^||Populates series related fields for entries, even without [wiki:Plugins/series series] plugin.||
||[wiki:Plugins/metainfo_imdb metainfo_imdb]||Detects imdb urls from description.||

^1. Not a builtin, configuration required to enable.^

== Command line plugins ==

||[wiki:Plugins/--cli-config --cli-config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugins/--dump --dump]||Display all entries after feed execution.||
||[wiki:Plugins/--feed --feed]||Executes only the specified feed(s)||
||[wiki:Plugins/--inject --inject]||Injects custom entry into feed(s).||
||[wiki:Plugins/try_regexp --try-regexp]||Test how regexps work on feed(s) interactively.||