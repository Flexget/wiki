# Plugins (for 0.9)

<h1 style="text-align: left; color: red">Note: 0.9.x is no longer maintained</h1>


[View latest plugins instead](/Plugins)

Due messy wiki (which is being re-organized) many plugin documentations are not available OR they have 1.0 specific features. You can use `flexget --doc <plugin>` to view FlexGet builtin documentation.

## Inputs
Produce [entries](/Entry) from external source.


| **Keyword** | **Description** |
| --- | --- |
| [rss](/InputRSS) | Parse RSS-feed. |
| [html](/InputHtml) | Parse any HTML-page. |
| [csv](/InputCSV) | Parse any CSV-file from URL. |
| [text](/InputText) | Parse any text data from URL. |
| [rlslog](/InputRlsLog) | Parse [http://rlslog.net](/http://rlslog.net). |
| [scenereleases](/InputSceneReleases) | Parse [http://scenereleases.info](/http://scenereleases.info). |
| [tvt](/InputTVTorrents) | Parse [http://tvtorrents.com](/http://tvtorrents.com). |

## Filters
Filter, Reject or Accept feeds [entries](/Entry) based on given rules. Single feed may have any number of filters.


| **Keyword** | **Description** |
| --- | --- |
| [regexp](/FilterRegexp) | Reject, Accept and Filter content by using regular expression. |
| [imdb](/FilterImdb) | Accept movie entries based on imdb details. |
| [series](/FilterSeries) | Accept TV-serie episodes. Quality and episode number aware. |
| [exists](/FilterExists) | Reject entries based on existing files in filesystem. |
| [limit_new](/FilterLimitNew) | Allow only given number of entries to pass per execution. |
| [seen_movies](/FilterSeenMovies) | Rejects already downloaded movies (detected by imdb-link). |
| [seen](/FilterSeen) | Reject already downloaded entries. [Builtin](/Builtin) |
| [torrent_size](/FilterTorrentSize) | Reject torrents that do not meet size requirements. |
| [patterns](/FilterPatterns) | [Deprecated](/ToBeRemoved). Accept entries based on regexp. Non-matching entries are filtered. |
| [accept](/FilterUnconditionally) | [Deprecated](/ToBeRemoved). Accept entries based on regexp. |
| [ignore](/FilterIgnore) | [Deprecated](/ToBeRemoved). Reject entries based on regexp. |

If you plan to use multiple filters per feed, you should look [filter operations](/FilterOperations) to understand how filters co-operate.

## Outputs
Execute operation(s) to entries that pass trough filter(s).


| **Keyword** | **Description** |
| --- | --- |
| [download](/OutputDownload) | Download passed entries into given path. |
| [make_rss](/OutputRSS) | Generate RSS-feed file from passed entries. |
| [statistics](/OutputStatistics) | Output statistics about downloaded entries. |
| [subtitles](/OutputSubtitles) | Download subtitles for movies from [opensubtitles.com](http://opensubtitles.com). |
| [exec](/OutputExec) | Execute command for passed entries. |
| [email](/OutputEmail) | Send email when new content is passed. |

## Modify / Other

| **Keyword** | **Description** |
| --- | --- |
| [interval](/ModuleInterval) | Maintain minimum poll interval for a feed. |
| [cookies](/ModuleCookies) | Enable cookies for all HTTP-requests. |
| [headers](/ModuleHeaders) | Modify HTTP headers. |
| [extension](/ModifyExtension) | Force a file extension. |
| [remove_trackers](/ModifyRemoveTrackers) | Remove trackers from a torrent. |
| [cli_config](/ModuleCliConfig) | Allow using values from commandline in YML-configuration file. |
| [try_regexp](/ModuleTryRegexp) | Test how regexps work on feed(s) interactively. |
||[disable_builtins](/ModuleDisableBuiltins)||Disable builtin modules from a feed.||