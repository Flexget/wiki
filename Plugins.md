= Plugins =

Formerly known as modules.

{{{
#!html
<h1 style="text-align: left; color: red">This page is only for upcoming 1.0</h1>
}}}

Plugins provide most of the functionality in !FlexGet. Plugins usually create, manipulate or download [wiki:Entry entries]. Some modules change how !FlexGet operates.

Plugin is enabled by placing a keyword and required settings in a configuration file. Example [wiki:InputRSS rss-module] would be used by placing following line under feed. See [wiki:Configuration configuration] if you are not familiar with the structure.

{{{
rss: http://some.site.com/some_feed.rss
}}}

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
||[wiki:InputRSS rss]||Parse RSS-feed.||
||[wiki:InputHtml html]||Parse any HTML-page.||
||[wiki:InputCSV csv]||Parse any CSV-file||
||[wiki:InputText text]||Parse any text data||
||[wiki:InputRlsLog rlslog]||Parse [http://rlslog.net].||
||[wiki:InputSceneReleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:InputTVTorrents tvt]||Parse [http://tvtorrents.com].||

== Filters ==

Reject or Accept feeds [wiki:Entry entries] based on given rules. Single feed may have any number of filters.

||'''Keyword'''||'''Description'''||
||[wiki:FilterRegexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:FilterImdb imdb]||Accept movie entries based on imdb details.||
||[wiki:FilterSeries series]||Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:FilterExists exists]||Reject entries based on existing files in filesystem.||
||[wiki:FilterLimitNew limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:FilterSeenMovies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:FilterSeen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:FilterTorrentSize torrent_size]||Reject torrents that do not meet size requirements.||

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand how filters co-operate.

== Outputs ==

Execute operation(s) to entries that pass trough filter(s).

||'''Keyword'''||'''Description'''||
||[wiki:OutputDownload download]||Download passed entries into given path.||
||[wiki:OutputRSS make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:OutputStatistics statistics]||Output statistics about downloaded entries.||
||[wiki:OutputSubtitles subtitles]||Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:OutputExec exec]||Execute command for passed entries.||
||[wiki:OutputEmail email]||Send email when new content is passed.||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:ModuleSearch search]||Search for download URL from supported sites.||
||[wiki:ModulePathByExt path_by_ext]||Change (download) path based on file-type (extension).||
||[wiki:ModuleInterval interval]||Maintain minimum poll interval for a feed.||
||[wiki:ModuleHeaders headers]||Modify HTTP headers.||
||[wiki:ModifyExtension extension]||Force a file extension.||
||[wiki:ModifyRemoveTrackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:ModuleCliConfig cli_config]||Allow using values from commandline in YML-configuration file.||
||[wiki:ModuleTryRegexp try_regexp]||Test how regexps work on feed(s) interactively.||
||[wiki:ModuleDisableBuiltins disable_builtins]||Disable builtin modules from a feed.||