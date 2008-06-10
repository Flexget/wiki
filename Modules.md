= Modules =

Modules provide all functionality to !FlexGet by creating, manipulating or downloading [wiki:Entry entries]. 

Module is enabled by placing keyword and parameters it requires in a configuration file. Example [wiki:InputRSS rss-module] would be used by placing following line under feed. See [wiki:Configuration configuration] if you are not familiar with the structure.

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
||[wiki:FilterPatterns patterns]||Accept entries based on regexp. Non-matching entries are filtered.||
||[wiki:FilterUnconditionally accept]||Accept entries based on regexp.||
||[wiki:FilterIgnore ignore]||Reject entries based on regexp.||
||[wiki:FilterImdb imdb]||Accept movie entries based on imdb details.||
||[wiki:FilterSeries series]||Accept TV-serie episodes. Quality and episode number aware.||
||[wiki:FilterExists exists]||Reject entries based on existing files in filesystem.||
||[wiki:FilterLimitNew limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:FilterSeenMovies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:FilterSeen seen]||Reject already downloaded entries (always enabled).||
||[wiki:FilterTorrentSize torrent_size]||Reject torrents that do not meet size requirements.||

=== Outputs ===

Execute actual operation after input has provided entries and filters have chosen what we are interested about.

||'''Keyword'''||'''Description'''||
||[wiki:OutputDownload download]||Download entries and store them in filesystem.||
||[wiki:OutputRSS make_rss]||Generate RSS-feed from passed entries.||
||[wiki:OutputStatistics statistics]||Output statistics about downloaded entries.||
||[wiki:OutputSubtitles subtitles]||Download subtitles for movies from [http://opensubtitles.com opensubtitles.com].||
||[wiki:OutputExec exec]||Execute command for entries reaching output.||

=== Modify / Other ===

||'''Keyword'''||'''Description'''||
||[wiki:ModuleCookies cookies]||Enable cookies for all http-requests.||
||[wiki:ModifyExtension extension]||Force file extension.||
||[wiki:ModifyRemoveTrackers remove_trackers]||Remove trackers from torrent.||
||[wiki:ModuleCliConfig cli_config]||Allow using variables in YML-configuration file and set values trough commandline.||

=== TODO ===

[wiki:FilterPatternsV2 patterns v2]

=== Notes ===

All examples in modules are assumed to be under feed. They are not sufficient alone. Look at [wiki:Configuration configuration] or complete examples if you have any open questions.

If you plan to use multiple filters per feed, you should look [wiki:FilterOperations filter operations] to understand how filters co-operate.

== So how does it all work? ==

Let's look real world configuration file.

{{{
feeds:
  tvrss combined:
    rss: http://tvrss.net/feed/unique/
    patterns:
      - south.park
    download: ~/torrents

  vegapunk:
    rss: http://bt.vegapunk.com/rss/rss.xml
    patterns:
      - ^\[vegapunk\].*one.piece.*\d\d\d.HD  
    download: ~/torrents
}}}

Here we have a simple configuration file with two feeds called {{{tvrss combined}}}
and {{{vegapunk}}}. Both have single input module [wiki:InputRSS RSS] that expects url as a parameter.
This converts RSS into [wiki:entry entries] for our feed. 

Next we have filter module [wiki:FilterPatterns patterns]
that expects list of regular expressions. If [wiki:entry] matches to any of these it will be accepted, if not then patterns module will issue filter command on it.
Last we have download module that simply downloads all remaining [wiki:Entry entries] and saves them to given path.

== Builtin modules (advanced users) ==

Some modules are always enabled even when they are not mentioned in configuration file. This is because they're
needed in almost all situations ([wiki:FilterSeen seen]) or they make sure specific content is formatted 
properly and do not intervene in other cases ([wiki:ModifyTorrent torrent]).

=== How to disable builtins ===

{{{
disable_builtins: true
}}}