= Modules =

Modules provide most of the functionality in !FlexGet. Modules usually create, manipulate or download [wiki:Entry entries]. Some modules change how !FlexGet operates.

Module is enabled by placing a keyword and required settings in a configuration file. Example [wiki:InputRSS rss-module] would be used by placing following line under feed. See [wiki:Configuration configuration] if you are not familiar with the structure.

{{{
rss: http://some.site.com/some_feed.rss
}}}

Execute !FlexGet with parameter {{{--list}}} to get list of all available modules. You can also view built-in module documentation by using parameter {{{--doc <keyword>}}}.

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

=== Filters ===

Filter, Reject or Accept feeds [wiki:Entry entries] based on given rules. Single feed may have any number of filters.

||'''Keyword'''||'''Description'''||
||[wiki:FilterPatterns patterns]||Accept entries based on regexp. Non-matching entries are filtered. [wiki:ToBeRemoved Deprecated]||
||[wiki:FilterUnconditionally accept]||Accept entries based on regexp. [wiki:ToBeRemoved Deprecated]||
||[wiki:FilterIgnore ignore]||Reject entries based on regexp. [wiki:ToBeRemoved Deprecated]||
||[wiki:FilterRegexp regexp]||Second generation regexp filtering module, will replace accept, patterns and ignore modules in future.||
||[wiki:FilterImdb imdb]||Accept movie entries based on imdb details.||
||[wiki:FilterSeries series]||Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:FilterExists exists]||Reject entries based on existing files in filesystem.||
||[wiki:FilterLimitNew limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:FilterSeenMovies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:FilterSeen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:FilterTorrentSize torrent_size]||Reject torrents that do not meet size requirements.||

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand how filters co-operate.

=== Outputs ===

Execute operation(s) to entries that pass trough filter(s).

||'''Keyword'''||'''Description'''||
||[wiki:OutputDownload download]||Download passed entries into given path.||
||[wiki:OutputRSS make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:OutputStatistics statistics]||Output statistics about downloaded entries.||
||[wiki:OutputSubtitles subtitles]||Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:OutputExec exec]||Execute command for passed entries.||
||[wiki:OutputEmail email]||Send email when new content is passed.||

=== Modify / Other ===

||'''Keyword'''||'''Description'''||
||[wiki:ModuleSearch search]||Search for download URL from supported sites.||
||[wiki:ModuleInterval interval]||Maintain minimum poll interval for a feed.||
||[wiki:ModuleCookies cookies]||Enable cookies for all HTTP-requests.||
||[wiki:ModifyExtension extension]||Force a file extension.||
||[wiki:ModifyRemoveTrackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:ModuleCliConfig cli_config]||Allow using values from commandline in YML-configuration file.||
||[wiki:ModuleTryRegexp try_regexp]||Test how regexps work on feed(s) interactively.||
||[wiki:ModuleDisableBuiltins disable_builtins]||Disable builtin modules from a feed.||

=== Notes ===

All examples in module documentations are assumed to be configured under a feed in configuration file. Look at [wiki:Configuration configuration] or complete examples if you're having troubles.

== So how does it all work? ==

Let's look real world configuration file.

{{{
feeds:
  tvrss combined:
    rss: http://tvrss.net/feed/unique/
    series:
      - south park
    download: ~/torrents

  vegapunk:
    rss: http://bt.vegapunk.com/rss/rss.xml
    patterns:
      - ^\[vegapunk\].*one.piece.*\d\d\d.HD
    download: ~/torrents

  baka:
    rss: 
      url: http://www.baka-updates.com/rss.php
      link: feedburner_origlink
      ascii: True
    regexp:
      accept:
        - SoulEaterFan.*Soul.Eater
        - ANBU.*Tytania.*HQ.*
      rest: filter
    download: ~/torrents
}}}

Here we have a simple configuration file with three feeds called {{{tvrss combined}}}, {{{vegapunk}}} and {{{baka}}}. They have a single input module [wiki:InputRSS RSS] that expects URL as a parameter.
This produces !FlexGet [wiki:Entry entries] from RSS feed. 

Vegapunk has a filter module [wiki:FilterPatterns patterns] that expects list of regular expressions. If [wiki:Entry entry] matches to any of these it will be accepted, if not then module will issue a filter command on it. TVRSS uses more sophisticated filter that is suitable for episodic tv-series called [wiki:FilterSeries series].

Baka uses the newer filter module [wiki:FilterRegexp regexp] that expects list of regular expressions to accept, reject or filter. In the example, if an [wiki:Entry entry] matches any of the patterns it will be accepted, if not then module places entry in filtered category. The regular expressions listed are loose and the patterns are searched across the entire strings, so a pattern like 'Soul' will match any [wiki:InputRSS RSS] with the word 'Soul' in it. It also uses parameters for the [wiki:InputRSS RSS] module to force the feed to ASCII and use a different RSS field for the torrent URL.

Last all the examples have a download module that simply downloads all remaining [wiki:Entry entries] and saves them to given path.