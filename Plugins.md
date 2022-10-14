---
title: Plugins
description: 
published: true
date: 2022-10-14T16:46:52.041Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:15.647Z
---

# Plugins
Plugins provide most of the functionality in FlexGet. Plugins usually create, manipulate or download **[entries](/Entry)** but they can also change how FlexGet operates. Many plugins can use the **[Jinja2 ](/Jinja)** template system.

Most plugins are enabled by placing a keyword and required settings in a configuration file. All plugins listed below are included in the FlexGet package (with the exception of the third-party plugins section). 

This documentation is meant for the latest released version. If you are upgrading from an older version, see [upgrade actions](/UpgradeActions) and the [changelog](/ChangeLog) for help in migrating your configuration file.

## Indentation in examples
All configuration examples are assumed to be placed under the `tasks` (or `templates`) [top-level keys](/Configuration#top-level-keys). If the documentation has this example:

```yaml
series:
  - name
```

In a full configuration, this goes into:

```yaml
tasks:
  task_name:
    rss: http://example.com
    series:
      - name
```

This makes examples more compact and reduces unnecessary boilerplate.

For further help with YAML and indenting, see [configuration](/Configuration).

## Plugin Types
- [Input](#input)
- [Filter](#filter)
- [Output](#output)
- [Metadata](#metadata)
- [Modification](#modification)
- [Daemon](#daemon)
- [Command Line Interface (CLI)](#command-line-interface)
- [Third-Party Plugins](#third-party-plugins)
- [Deprecated](#deprecated)


## Input
Produce **[entries](/Entry)** from external source.  
Most requests are cached so there is no penalty for using the same RSS URL multiple times in the configuration, for example.

**Note:** If you are looking for torrent search plugins, refer to [Search Plugins](/Searches).

### Raw Input
Input plugins that directly parse data from a source based on its type.

| **Keyword** | **Description** |
| --- | --- |
| [csv](/Plugins/csv) | Parse any CSV-file |
| [filesystem](/Plugins/filesystem) | Search through a local directory looking for files as a input.  |
| [html](/Plugins/html) | Parse any HTML-page. |
| [limit](/Plugins/limit) | Limit the amount of entries created by another input plugin. |
| [rss](/Plugins/rss) | Parse RSS-feed. |
| [sftp_list](/Plugins/sftp_list) | List files from an SFTP server |
| [search_rss](/Plugins/search_rss) | Search with parametrized rss feed. |
| [tail](/Plugins/tail) | Tail a log file (eg. irc logs) |
| [text](/Plugins/text) | Parse any text data |
| [regexp_parse](/Plugins/regexp_parse) | Use regular expressions to parse text from a web resource or file |
| [ftp_list](/Plugins/ftp_list) | Lists the content of a remote FTP server |

### 3rd party sites input
Input plugins designed to retrieve data from 3rd party web-sites, such as IMDB, trakt & etc.

| Keyword | Description |
| --- | --- |
| [anidb_list](/Plugins/anidb_list) | Create entries from your AniDB wishlist. |
| [anilist](/Plugins/anilist) | Create entries from your AniList watchlist. |
| [apple_trailers](/Plugins/apple_trailers) | Get movie trailers from Apple.com |
| [betaseries_list](/Plugins/betaseries_list) | Use series you follow on www.betaseries.com as an input |
| [from_imdb](/Plugins/from_imdb) | Produce entries based on an IMDB person, company or character  |
| [kitsu](/Plugins/kitsu) | Produce Entries based on your  [Kitsu.io](http://kitsu.io) libraries. |
| [imdb_list](/Plugins/List/imdb_list) | Use movies in your IMDb list as an input (eg. watchlist, rating history). [Managed List](/Plugins/List).<br> **Note:** This plugin does not currently work, look into [`imdb_watchlist`](/Plugins/imdb_watchlist) |
| [filmweb_watchlist](/Plugins/filmweb_watchlist) | Use your Filmweb wathlist as an input
| [imdb_watchlist](/Plugins/imdb_watchlist) |Use you IMDB watchlist as an input|
| [letterboxd](/Plugins/letterboxd) | Create entries for movies on any public [Letterboxd](http://letterboxd.com) list |
| [magnetdl](/Plugins/magnetdl) | Create entries from magnetdl.com |
| [my_anime_list](/Plugins/my_anime_list) | Create entries from MyAnimeList animelist. |
| [myepisodes_list](/Plugins/myepisodes_list) | Create entries from the shows in your myepisodes.com account. |
| [npo_watchlist](/Plugins/npo_watchlist) | Create entries for the shows and episodes in your npo.nl account (Dutch public television). |
| [pogcal](/Plugins/pogcal) | Produce entries for shows marked on your [pogdesign calendar](http://www.pogdesign.co.uk/cat/). |
| [rottentomatoes_list](/Plugins/rottentomatoes_list) | Use movies from [Rotten Tomatoes](http://www.rottentomatoes.com) lists. |
| [sceper](/Plugins/sceper) | Parse [http://sceper.ws](http://sceper.ws). |
| [thetvdb_list ](/Plugins/List/thetvdb_list) | Produce an entry for all shows you have marked as favorites at http://thetvdb.com. [Managed List](/Plugins/List) |
| [next_trakt_episodes](/Plugins/next_trakt_episodes) | Create entries for the latest or the next episode to watch or collect by your trakt.tv activity. |
| [trakt_list](/Plugins/List/trakt_list) | Create entries from one of your trakt.tv lists. [Managed List](/Plugins/List) |
| [twitterfeed](/Plugins/twitterfeed) | Create entries from a twitter account. |
| [lostfilm](/Plugins/lostfilm) | Create entries from lostfilm.tv |

### 3rd party software input
Input plugins designed to retrieve data from 3rd party software, such as Sonarr, couchpotato, deluge & etc.

| Keyword | Description |
| --- | --- |
| [couchpotato_list ](/Plugins/List/couchpotato_list) | Produce entries from couchpotato wanted movies list. [Managed List](/Plugins/List) |
| [from_deluge](/Plugins/from_deluge) | Use torrents loaded in a Deluge daemon as input. |
| [from_rtorrent](/Plugins/rtorrent) | Use torrents loaded in a rTorrent as input. |
| [from_transmission](/Plugins/from_transmission) | Use torrents loaded in Transmission as input. |
| [plex](/Plugins/plex) | Produce entries for shows present in a [Plex Media Server](http://www.plexapp.com) section. |
| [radarr_list](/Plugins/Lists/radarr_list) | Produce entries from or to radarr_list. [Managed List](/Plugins/List) |
| [sickbeard](/Plugins/sickbeard) | Produce entries from Sickbeard's show list |
| [sonarr_list](/Plugins/List/sonarr_list) | Produce entries from Sonarr's show list. [Managed List](/Plugins/List) |
| [next_sonarr_episodes](/Plugins/next_sonarr_episodes) | Produce entries for missing episodes from Sonarr |
| [medusa](/Plugins/Medusa) |  Produce entries from Medusa's show list |

### Internal Input
Input plugins that will generate entries based on preexisting data in FlexGet.

| Keyword | Description |
| --- | --- |
| [configure_series](/Plugins/configure_series) | Configures the series plugin with all the shows given by any input plugin (eg. filesystem, rss).  |
| [discover](/Plugins/discover) | Produce entries from search results. |
| [from_digest](/Plugins/from_digest) | Outputs entries which have been collected by the [digest](/Plugins/digest) plugin. |
| [from_task](/Plugins/from_task) | Runs another task and outputs accepted entries from that task. |
| [next_series_episodes](/Plugins/next_series_episodes) | Emits the next episode needed for each series configured in the series plugin. Useful for example with [discover](/Plugins/discover). |
| [next_series_seasons](/Plugins/next_series_seasons) | Emits the next season needed for each series configured in the series plugin. Useful for example with [discover](/Plugins/discover). |
| [inputs](/Plugins/inputs) | Configure the same input plugin multiple times in one task. |
| [entry_list](/Plugins/List/entry_list) | Use or add entries to a custom made entry list. [Managed List](/Plugins/List) |
| [movie_list](/Plugins/List/movie_list) | Use or add entries to a custom made movie list. [Managed List](/Plugins/List) |
| [subtitle_list](/Plugins/List/subtitle_list) | Use or add entries to a custom made subtitle list. [Managed List](/Plugins/List) |
| [pending_list](/Plugins/List/pending_list) | Manually approve entries |

## Filter
Reject or Accept **[entries](/Entry)** based on given rules. A single task may have any number of filters.  
If you plan to use multiple filters per task, you should look at **[filtering operations](/Filtering)** to understand how they work.

### Content based filters
Filters based on the nature of the input content (such as movie, series, series premiere & etc.)

| **Keyword** | **Description** |
| --- | --- |
| [all_series](/Plugins/all_series) | Accepts any entry that appears to be an episode of a series. |
| [proper_movies](/Plugins/proper_movies) | Keep track of downloaded movies and force re-download proper versions. |
| [series](/Plugins/series) | Accept TV-series episodes. Quality and episode number aware. |
| [series_premiere](/Plugins/series_premiere) | Accept any entry that appears to be the first episode of a series. |
| [list_match ](/Plugins/List/list_match) | Use this plugin to filter entries based on another list plugin. |

### Metadata filters
Filters based on content's metadata such as size and quality

| **Keyword** | **Description** |
| --- | --- |
| [best_quality](/Plugins/best_quality) | Group entries by identifier and accept/reject best/worse qualities within these groups. |
| [content_size](/Plugins/content_size) | Reject torrents and nzb's that do not meet size requirements. |
| [quality](/Plugins/quality) | Reject entries not of the specified quality. |

### FlexGet internal filters
Filters based on preexisting data or operations within FlexGet

| **Keyword** | **Description** |
| --- | --- |
| [upgrade](/Plugins/upgrade) | Accept/Reject better qualities of an entry (tracked by a unique identifier) |
| [timeframe](/Plugins/timeframe) | Timeframe in which FlexGet waits for the chosen quality. |
| [duplicates](/Plugins/duplicates) | Perform action based on duplicate entries by a field. |
| [limit_new](/Plugins/limit_new) | Allow only given number of entries to pass per execution. |
| [only_new](/Plugins/only_new) | Causes all entries that were in the task on the previous run to be rejected at the input phase. |
| [require_field](/Plugins/require_field) | Reject entries that do not have the specified fields. |
| [seen_movies](/Plugins/seen_movies) | Rejects already downloaded movies (detected by imdb-link). |
| [seen](/Plugins/seen) | Reject already downloaded entries. [Builtin](/Builtin) |

### Torrent specific filters
Filters based specifically for torrents

| **Keyword** | **Description** |
| --- | --- |
| [content_filter](/Plugins/content_filter) | Reject based on filenames within torrents. |
| [magnets](/Plugins/magnets) | Rejects entries with only magnet links. |
| [private_torrents](/Plugins/private_torrents) | Reject private or public torrents. |
| [seen_info_hash](/Plugins/seen_info_hash) | Rejects already downloaded torrents (detected by torrent info hash). [Builtin](/Builtin) |
| [torrent_alive](/Plugins/torrent_alive) | Reject any torrents that do not have an active tracker with seeds. |

### Logical and operational filters
Filters that will accept/reject entries based on logical statements or simple file operations

| **Keyword** | **Description** |
| --- | --- |
| [accept_all](/Plugins/accept_all) | Accept all entries. |
| [age](/Plugins/age) | Reject, Accept entries based on age by looking at a date in a specified entry field. |
| [archives](/Plugins/archives) | Accept, reject entries based on if they're valid ZIP/RAR archives. |
| [crossmatch](/Plugins/crossmatch) | Accept/reject based on other inputs (eg. imdb_list watchlist, ratings history). |
| [exists](/Plugins/exists) | Reject entries based on existing files in filesystem. |
| [exists_movie](/Plugins/exists_movie) | Reject entries based on existing movies in filesystem. |
| [exists_series](/Plugins/exists_series) | Reject entries based on existing series in filesystem. |
| [if](/Plugins/if) | Filter based on simple python statements. |
| [regexp](/Plugins/regexp) | Reject, Accept entries by using regular expression. |

### 3rd party sites filters
Filters based on data retrieved from 3rd party sites

| **Keyword** | **Description** |
| --- | --- |
| [imdb](/Plugins/imdb) | Accept movie entries based on imdb details. |
| [rottentomatoes](/Plugins/rottentomatoes) | Accept movie entries based on Rotten Tomatoes details. |

## Output
Execute operation(s) on accepted entries.

### 3rd party software output
Send accepted entries to 3rd party software, usually downloaders.

| **Keyword** | **Description** |
| --- | --- |
| [aria2](/Plugins/aria2) | Pass URIs to be downloaded to the aria2 downloader. |
| [deluge](/Plugins/deluge) | Pass torrents directly to deluge bittorrent client, supporting magnet links. |
| [nzbget](/Plugins/nzbget) | Download nzbs with nzbget. |
| [periscope](/Plugins/periscope) | Download subtitles with Periscope. |
| [pyload](/Plugins/pyload) | http://pyload.net/. |
| [qbittorrent](/Plugins/qbittorrent) | Pass torrents directly to the qBittorrent client, supporting magnet links. |
| [rtorrent](/Plugins/rtorrent) | Pass torrents directly to rtorrent |
| [rtorrent_magnet](/Plugins/rtorrent_magnet) | Handles magnet URI's and produces rTorrent compatible torrent files (0.8.9+) |
| [sabnzbd](/Plugins/sabnzbd) | Download nzbs with SABnzbd. |
| [subliminal](/Plugins/subliminal) | Download subtitles with Subliminal. |
| [transmission](/Plugins/transmission) | Pass torrents directly to transmission, supporting magnet links. |
| [utorrent](/Plugins/utorrent) | Pass torrents directly to uTorrent. |

### 3rd party sites output
Send accepted entries to 3rd party sites, usually for tracking purposes. 

| **Keyword** | **Description** |
| --- | --- |
| [myepisodes](/Plugins/myepisodes) | Mark accepted episodes as acquired on MyEpisodes. |
| [pogcal_acquired](/Plugins/pogcal_acquired) | Mark accepted episodes on [pogdesign TV calendar](http://pogdesign.co.uk/cat) |
| [kodi_library](/Plugins/kodi_library) | Send clean/scan requests to a remote/local Kodi server. |

### Notifier services output
Send accepted entries to notification services. More details [here](/Plugins/Notifiers).

| **Keyword** | **Description** |
| --- | --- |
| [email](/Plugins/Notifiers/email) | Send an email message |
| [gotify](/Plugins/Notifiers/gotify) | Send a [Gotify](https://gotify.net) notification |
| [join](/Plugins/Notifiers/join) | Send a [Join](https://joaoapps.com/join/) notification |
| [notify_osd](/Plugins/Notifiers/notify_osd) | Send a [NotifyOSD](https://wiki.ubuntu.com/NotifyOSD) notification |
| [notifymyandroid](/Plugins/Notifiers/notifymyandroid) | Send a [NMA](http://www.notifymyandroid.com/) notification |
| [mqtt](/Plugins/Notifiers/mqtt) | Send MQTT notification |
| [prowl](/Plugins/Notifiers/prowl) | Send a [Prowl](https://www.prowlapp.com/) notification |
| [pushalot](/Plugins/Notifiers/pushalot) | Send a [Pushalot](https://pushalot.com/) notification |
| [pushbullet](/Plugins/Notifiers/pushbullet) | Send a [Pushbullet](https://www.pushbullet.com/) notification |
| [pushover](/Plugins/Notifiers/pushover) | Send a [Pushover](https://pushover.net/apps/clone/Flexget) notification |
| [pushsafer](/Plugins/Notifiers/pushsafer) | Send a [Pushsafer](https://www.pushsafer.com/en/FlexGet) notification |
| [rapidpush](/Plugins/Notifiers/rapidpush) | Send a [Rapidpush](https://rapidpush.net/) notification |
|[discord](/Plugins/Notifiers/discord) | Send a [Discord](https://discordapp.com/) notification
| [slack](/Plugins/Notifiers/slack) | Send a [Slack](https://slack.com/) notification |
| [sms_ru](/Plugins/Notifiers/sms_ru) | Send a [SMS.RU](http://sms.ru/) notification |
| [sns](/Plugins/Notifiers/sns) | Send a [SNS](https://aws.amazon.com/sns/) notification |
| [telegram](/Plugins/Notifiers/telegram) | Send a [Telegram](https://telegram.org/) notification |
| [xmpp](/Plugins/Notifiers/xmpp) | Send an [XMPP](https://xmpp.org/) notification |
| [ms_teams](/Plugins/Notifiers/ms_teams) |Send a [Microsoft Teams](https://products.office.com/en-us/microsoft-teams/group-chat-software) notification |

### FlexGet internal output
Use accepted entries as an input for various FlexGet plugins such as add to movie queue, set series begin & etc.

| **Keyword** | **Description** |
| --- | --- |
| [digest](/Plugins/digest) | Collects entries from tasks to be combined into another task (usually for notification.) |
| [series_remove](/Plugins/series_remove) | Remove accepted series \ episodes from the [series](/Plugins/series) plugin |
| [set_series_begin](/Plugins/set_series_begin) | Set the first episode to download for series. |
| [list_add](/Plugins/List/list_add) | Use this plugin to add accepted entries to another list plugin. |
| [list_remove](/Plugins/List/list_remove) | Use this plugin to remove accepted entries to another list plugin. |

### File operations output
Perform different file operations using accepted entries.

| **Keyword** | **Description** |
| --- | --- |
| [copy](/Plugins/copy) | Copy local files. |
| [decompress](/Plugins/decompress) | Extract Zip and RAR files. |
| [delete](/Plugins/delete) | Delete local files. |
| [download](/Plugins/download) | Download passed entries into given path. |
| [exec](/Plugins/exec) | Executes commands on entries. |
| [ftp_download](/Plugins/ftp_download) | Download entries retrieved from [ftp_list](/Plugins/ftp_list) |
| [move](/Plugins/move) | Move local files. |
| [sftp_download](/Plugins/sftp_download) | Download files from an SFTP server |
| [sftp_upload](/Plugins/sftp_upload) | Upload files to an SFTP server |
| [symlink](/Plugins/symlink) | Symlink local files. |

### Generators output
Generate custom output using accepted entries.

| **Keyword** | **Description** |
| --- | --- |
| [make_html](/Plugins/make_html) | Generate HTML file from passed entries. |
| [make_rss](/Plugins/make_rss) | Generate RSS-feed file from passed entries. |

## Metadata
Retrieve additional data from internal parsers or 3rd party sites. Used for population of more fields than default or to actively perform data retrieval for specific input types.

These provide metainfo (ie. fields) to [Entry](/Entry).

| Keyword | Description |
| --- | --- |
| [imdb_lookup](/Plugins/imdb_lookup) | Enable imdb parsing for imdb fields on-demand. |
| [rottentomatoes_lookup](/Plugins/rottentomatoes_lookup) | Enable Rotten Tomatoes parsing for Rotten Tomatoes fields on-demand. |
| [thetvdb_lookup](/Plugins/thetvdb_lookup) | Fetch series information from http://thetvdb.com/ |
| [tmdb_lookup](/Plugins/tmdb_lookup) | Enable http://www.themoviedb.org/ parsing for tmdb fields on-demand. |
| [torrent_files](/Plugins/torrent_files) | Builtin. Parse torrent files for metadata |
| [trakt_lookup](/Plugins/trakt_lookup) | Enable http://trakt.tv/ parsing for trakt fields on-demand. |
| [tvmaze_lookup](/Plugins/tvmaze_lookup) | Enable http://tvmaze.com/ parsing for tvmaze fields on-demand. |
| [bluray_lookup](/Plugins/bluray_lookup) | Enable http://m.blu-ray.com/ parsing for bluray fields on-demand. |
| [nfo_lookup](https://flexget.com/Plugins/nfo_lookup) | Read movie information from an [nfo file](http://kodi.wiki/view/NFO_files) (specially useful for [Kodi](https://kodi.tv/) libraries).
| [check_subtitles](/Plugins/check_subtitles) | Check subtitles presence for local files. |
| [metainfo_movie](/Plugins/metainfo_movie) | Call internal movie parser to parse task entries and generated movie related data. |
| [metainfo_series](/Plugins/metainfo_series) | Use internal series parser to parse task entries and generated series related data. |

## Modification
Plugins that can manipulate data and perform various operations.

### Request operations
Perform various operations on request that are being sent and received. 

| **Keyword** | **Description** |
| --- | --- |
| [cfscraper](/Plugins/cfscraper) | Enables cloudflare scraping in a task. |
| [convert_magnet](/Plugins/convert_magnet) | Converts magnet uris to torrent files using libtorrent |
| [cookies](/Plugins/cookies) | Use FireFox3 cookies. |
| [domain_delay](/Plugins/domain_delay) | Sets a minimum interval between requests to specific domains. |
| [formlogin](/Plugins/formlogin) | Log in to web site via login form. |
| [headers](/Plugins/headers) | Modify HTTP headers. |
| [proxy](/Plugins/proxy) | Use a proxy to access resources. |
| [urlrewrite_search](/Plugins/urlrewrite_search) | Search for download URL from supported sites by using entry title. |

### 3rd Party Site Request Operations

| **Keyword** | **Description** |
| --- | --- |
| [wp_auth](/Plugins/wp_auth) | Access WordPress [s2Member](https://s2member.com/) protected RSS feeds. |
| [rutracker](/Plugins/rutracker) | Supports downloading torrents from rutracker. |


### File operations
Perform file oriented operations.


| **Keyword** | **Description** |
| --- | --- |
| [add_trackers](/Plugins/add_trackers) | Add trackers to torrents. |
| [extension](/Plugins/extension) | Force a file extension. |
| [free_space](/Plugins/free_space) | Abort task when drive space is low. |
| [path_by_ext](/Plugins/path_by_ext) | Change (download) path based on file-type (extension). |
| [path_by_space](/Plugins/path_by_space) | Select a path based on disk stats |
| [remove_trackers](/Plugins/remove_trackers) | Remove trackers from a torrent. |
| [set](/Plugins/set) | Set 'path' or other info per task. Can be dynamic per entry. |

### Data operations
Manipulate relevant data based on input.

| **Keyword** | **Description** |
| --- | --- |
| [assume_quality](/Plugins/assume_quality) | Make assumptions about the qualities of releases. |
| [manipulate](/Plugins/manipulate) | Allows regexp manipulation for entries. |
| [parsing](/Plugins/parsing) | Configure another parser for series and movie titles. (can help if IMDB/TMDB/TVDB lookup fails too often) |
| [pathscrub](/Plugins/pathscrub) | Cleans invalid characters from generated path/file names. (Used by other plugins that generate files.) |
| [torrent_scrub](/Plugins/torrent_scrub) | Removes non-standard keys like libtorrent resume information from downloads (which prevents the torrent from properly starting in Rtorrent). |
| [urlrewrite](/Plugins/urlrewrite) | User regexp for URL Rewriting. |
| [rmz](/Plugins/rmz)| URL rewrite plugin for rmz.cr rss feed. Filehoster links to be grabbed can be configured.
| [rlsbb](/Plugins/rlsbb)| URL rewrite plugin for rlsbb.ru rss feed. Filehoster links to be grabbed and comment parsing can be configured.

### FlexGet internal operations
Perform various FlexGet operations.

| **Keyword** | **Description** |
| --- | --- |
| [archive](/Plugins/archive) | Archive all seen entries for searchable database for later retrieval. |
| [delay](/Plugins/delay) | Adds artificial delay into a task. |
| [disable](/Plugins/disable) | Disable builtin plugin(s) from a task, or plugins included from a template. |
| [include](/Plugins/include) | Include configuration from another yaml file. |
| [interval](/Plugins/interval) | Maintain minimum poll interval for the task. |
| [log_filter](/Plugins/log_filter) | Filter prevent certain messages from being logged. |
| [manual](/Plugins/manual) | Only run the task when explicitly specified. |
| [max_reruns](/Plugins/max_reruns) | Limit the maximum number of task reruns. |
| [no_entries_ok](/Plugins/no_entries_ok) | Silence warnings about task not producing entries, for tasks where that is normal. |
| [priority](/Plugins/priority) | Change task execution order. |
| [plugin_priority](/Plugins/plugin_priority) | Change plugin priorities. |
| [remember_rejected](/Plugins/remember_rejected) | Remember rejections and reject them in future runs. |
| [reorder_quality](/Plugins/reorder_quality) | Reorder [qualities](../Qualities) to make one quality better or worse than another. |
| [retry_failed](/Plugins/retry_failed) | Save failed entries so they can be retried. [Builtin](/Builtin) |
| [run_task](/Plugins/run_task) | Trigger exectution of another task.
| [variables](/Plugins/variables) | Replace specific jinja2 values in config before executing tasks. |
| [sequence](/Plugins/sequence) | Allows the same plugin to be configured multiple times in a task. |
| [sleep](/Plugins/sleep) | Causes a pause to occur at a specified point during task execution. |
| [sort_by](/Plugins/sort_by) | Sort entries in a task. |
| [template](/Plugins/template) | Provides global configuration and named templates. |
| [verify_ssl_certificates](/Plugins/verify_ssl_certificates) | Can turn off SSL certificate verification on a task. |
| [version_checker](/Plugins/version_checker) | Checks if user is running latest Flexget version on a given interval. |

## Daemon
These plugins are specifically for when FlexGet is being used in daemon mode. They differ from the other plugins documented here, in that they should be configured at the root of your config. Not inside any tasks or templates.

| **Keyword** | **Description** |
| --- | --- |
| [scheduler](/Plugins/Daemon/scheduler) | Executes tasks with a given interval or schedule while daemon is running. |
| [irc](/Plugins/Daemon/irc) | Connect a bot to an IRC channel and act on tracker announcements.|

## Command Line Interface
Use `flexget --help` for full list of subcommands. `--help` can also be used with any of the subcommands for further help text.

| Command | Description |
| --- | --- |
| [inject](/Plugins/cli/inject) | Inject entries into tasks from the CLI. |
| [service](/Plugins/cli/service) | **`EXPERIMENTAL`** A Windows service installer for the FlexGet daemon. |

### `execute` command options
Use `flexget execute --help` for full option list.

| Argument | Description |
| --- | --- |
| [--cli-config](/Plugins/--cli-config) | Allow using values from commandline in YML-configuration file. |
| [--dump](/Plugins/--dump) | Display all entries after task execution. |
| [--tasks](/Plugins/--tasks) | Executes only the specified task(s) |
| [--inject](/Plugins/--inject) | Injects custom entry into task(s). |
| [--try-regexp](/Plugins/try_regexp) | Test how regexps work on task(s) interactively. |

## Third-party plugins
Plugins can be installed by simply placing them in a `plugins` folder alongside your configuration file. (This would usually be `~/.flexget/plugins/`, however it may be different if your config is in a different [location](https://www.flexget.com/Configuration#location).) It is also possible to package plugins in a separate Python package like [FlexGet extras](https://github.com/Flexget/extras).

There is a list of [third-party and extra plugins](/Plugins/ThirdPartyExtras) available, which are plugins that are not common, actively maintained or are otherwise unsuitable for main distribution.

## Deprecated
| Keyword | Description |
| --- | --- |
| [clean_transmission](/Plugins/clean_transmission) | Clean Transmission queue. |
|[emit_movie_queue](/Plugins/emit_movie_queue)|Emit your [movie_queue](/Plugins/movie_queue).|| 
| [movie_queue](/Plugins/movie_queue) | Accept movies from movie queue. |
| [subtitle_queue](/Plugins/subtitle_queue) | Add or accept files to get subtitles for. |
