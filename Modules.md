= Plugins (for 0.9) =

{{{
#!html
<h1 style="text-align: left; color: red">Note: 0.9.x is no longer maintained</h1>
}}}

[wiki:Plugins View latest plugins instead]

Due messy wiki (which is being re-organized) many plugin documentations are not available OR they have 1.0 specific features. You can use `flexget --doc <plugin>` to view !FlexGet builtin documentation.

== Inputs ==

Produce [wiki:Entry entries] from external source.

||'''Keyword'''||'''Description'''||
||[wiki:InputRSS rss]||Parse RSS-feed.||
||[wiki:InputHtml html]||Parse any HTML-page.||
||[wiki:InputCSV csv]||Parse any CSV-file from URL.||
||[wiki:InputText text]||Parse any text data from URL.||
||[wiki:InputRlsLog rlslog]||Parse [http://rlslog.net].||
||[wiki:InputSceneReleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:InputTVTorrents tvt]||Parse [http://tvtorrents.com].||

== Filters ==

Filter, Reject or Accept feeds [wiki:Entry entries] based on given rules. Single feed may have any number of filters.

||'''Keyword'''||'''Description'''||
||[wiki:FilterRegexp regexp]||Reject, Accept and Filter content by using regular expression.||
||[wiki:FilterImdb imdb]||Accept movie entries based on imdb details.||
||[wiki:FilterSeries series]||Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:FilterExists exists]||Reject entries based on existing files in filesystem.||
||[wiki:FilterLimitNew limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:FilterSeenMovies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:FilterSeen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:FilterTorrentSize torrent_size]||Reject torrents that do not meet size requirements.||
||[wiki:FilterPatterns patterns]||[wiki:ToBeRemoved Deprecated]. Accept entries based on regexp. Non-matching entries are filtered.||
||[wiki:FilterUnconditionally accept]||[wiki:ToBeRemoved Deprecated]. Accept entries based on regexp.||
||[wiki:FilterIgnore ignore]||[wiki:ToBeRemoved Deprecated]. Reject entries based on regexp.||

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
||[wiki:ModuleInterval interval]||Maintain minimum poll interval for a feed.||
||[wiki:ModuleCookies cookies]||Enable cookies for all HTTP-requests.||
||[wiki:ModuleHeaders headers]||Modify HTTP headers.||
||[wiki:ModifyExtension extension]||Force a file extension.||
||[wiki:ModifyRemoveTrackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:ModuleCliConfig cli_config]||Allow using values from commandline in YML-configuration file.||
||[wiki:ModuleTryRegexp try_regexp]||Test how regexps work on feed(s) interactively.||
||[wiki:ModuleDisableBuiltins disable_builtins]||Disable builtin modules from a feed.||