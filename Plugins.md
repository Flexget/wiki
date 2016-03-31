= Plugins =

{{{
#!comment

# just ready for important info

#!html
#<h1 style="text-align: left; color: red">Note: Plugins page is being re-organized so many links are not working</h1>
#<b>This page contains plugins that are available only on bleeding edge.</b> 
}}}

Plugins provide most of the functionality in !FlexGet. Plugins usually create, manipulate or download '''[wiki:Entry entries]''' but they can also change how !FlexGet operates. Many plugins can use the '''[wiki:Jinja Jinja2 ]''' template system.

Most plugins are enabled by placing a keyword and required settings in a configuration file. All plugins listed below are included in the !FlexGet package (with the exception of the third-party plugins section).

== Indentation in examples ==

All configuration examples are assumed to be placed under a task (or template.) So if documentation has this example:

{{{
series:
  - name
}}}

In a full configuration, this goes into:

{{{
tasks:
  task_name:
    rss: http://example.com
    series:
      - name
}}}

This makes examples more compact and reduces unnecessary boilerplate.


== Inputs ==


Produce '''[wiki:Entry entries]''' from external source.[[BR]]
Most requests are cached so there is no penalty for using the same RSS URL multiple times in the configuration, for example.

'''Note:''' If you are looking for torrent search plugins, refer to [wiki:Searches Search Plugins].


=== 3rd party sites input ===

Input plugins designed to retrieve data from 3rd party web-sites, such as IMDB, trakt & etc.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/anidb_list anidb_list]||`UPDATED` Create entries from your AniDB wishlist.||
||[wiki:Plugins/apple_trailers apple_trailers]||Get movie trailers from Apple.com||
||[wiki:Plugins/betaseries_list betaseries_list]||Use series you follow on www.betaseries.com as an input||
||[wiki:Plugins/dynamic_imdb dynamic_imdb ]|| `UPDATED` Dynamically produce entries based on an IMDB person, company or character ||
||[wiki:Plugins/imdb_list imdb_list]||`UPDATED` Use movies in your IMDb list as an input (eg. watchlist, rating history).||
||[wiki:Plugins/letterboxd letterboxd]||Create entries for movies on any public [http://letterboxd.com Letterboxd] list||
||[wiki:Plugins/myepisodes_list myepisodes_list]||Create entries from the shows in your myepisodes.com account.||
||[wiki:Plugins/pogcal pogcal]||Produce entries for shows marked on your [http://www.pogdesign.co.uk/cat/ pogdesign calendar].||
||[wiki:Plugins/rottentomatoes_list rottentomatoes_list]||Use movies from [http://www.rottentomatoes.com Rotten Tomatoes] lists.||
||[wiki:Plugins/sceper sceper]||Parse [http://sceper.ws].||
||[wiki:Plugins/thetvdb_favorites thetvdb_favorites]||Produce an entry for all shows you have marked as favorites at http://thetvdb.com.||
||[wiki:Plugins/trakt_emit trakt_emit]||Create entries for the latest or the next episode to watch or collect by your trakt.tv activity.||
||[wiki:Plugins/trakt_list trakt_list]||Create entries from one of your trakt.tv lists.||
||[wiki:Plugins/twitterfeed twitterfeed]||Create entries from a twitter account.||
||[wiki:Plugins/whatcd whatcd]||Produce entries for content on [https://what.cd]||

=== 3rd party software input ===

Input plugins designed to retrieve data from 3rd party software, such as Sonarr, couchpotato, deluge & etc.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/couchpotato_list couchpotato_list ]||Produce entries from couchpotato wanted movies list||
||[wiki:Plugins/from_deluge from_deluge]||Use torrents loaded in a Deluge daemon as input.||
||[wiki:Plugins/rtorrent from_rtorrent]||Use torrents loaded in a rTorrent as input.||
||[wiki:Plugins/from_transmission from_transmission]||Use torrents loaded in Transmission as input.||
||[wiki:Plugins/plex plex]||Produce entries for shows present in a [http://www.plexapp.com Plex Media Server] section.||
||[wiki:Plugins/sickbeard sickbeard]||Produce entries from Sickbeard's show list||
||[wiki:Plugins/sonarr_list sonarr_list ]||`UPDATED` Produce entries from Sonarr's show list||
||[wiki:Plugins/sonarr_emit sonarr_emit ]||Produce entries for missing episodes from Sonarr||
||[wiki:Plugins/uoccin_emit uoccin_emit ]||`NEW` Produce entries from a [https://github.com/tarzasai/Uoccin Uoccin] data file||

=== Internal Input ===

Input plugins that will generate entries based on preexisting data in !FlexGet.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/configure_series configure_series]||Configures the series plugin with all the shows given by any input plugin (eg. filesystem, rss). ||
||[wiki:Plugins/discover discover]||Produce entries from search results.||
||[wiki:Plugins/emit_digest emit_digest]||Outputs entries which have been collected by the [wiki:Plugins/digest digest] plugin.||
||[wiki:Plugins/emit_movie_queue emit_movie_queue]||`UPDATED` Emit your [wiki:Plugins/movie_queue movie_queue], useful for example with [wiki:Plugins/discover discover].||
||[wiki:Plugins/emit_series emit_series]||Emit the next episode needed for each series configured in the series plugin. Useful for example with [wiki:Plugins/discover discover].||
||[wiki:Plugins/inputs inputs]||Configure the same input plugin multiple times in one task.||

=== Raw Input ===

Input plugins that directly parse data from a source based on its type.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/csv csv]||Parse any CSV-file||
||[wiki:Plugins/filesystem filesystem]||Search through a local directory looking for files as a input. ||
||[wiki:Plugins/html html]||Parse any HTML-page.||
||[wiki:Plugins/rss rss]||Parse RSS-feed.||
||[wiki:Plugins/sftp_list sftp_list]||List files from an SFTP server||
||[wiki:Plugins/tail tail]||Tail a log file (eg. irc logs)||
||[wiki:Plugins/text text]||Parse any text data||
||[wiki:Plugins/regexp_parse regexp_parse]||Use regular expressions to parse text from a web resource or file||
||[wiki:Plugins/ftp_list ftp_list]||Lists the content of a remote FTP server||

== Filters ==

Reject or Accept '''[wiki:Entry entries]''' based on given rules. A single task may have any number of filters.[[BR]]
If you plan to use multiple filters per task, you should look at '''[wiki:Filtering filtering operations]''' to understand how they work.

=== Content based filters ===

Filters based on the nature of the input content (such as movie, series, series premiere & etc.)
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/all_series all_series]||Accepts any entry that appears to be an episode of a series.||
||[wiki:Plugins/movie_queue movie_queue]||`UPDATED` Accept movies from movie queue.||
||[wiki:Plugins/proper_movies proper_movies]||Keep track of downloaded movies and force re-download proper versions.||
||[wiki:Plugins/series series]||Accept TV-series episodes. Quality and episode number aware.||
||[wiki:Plugins/series_premiere series_premiere]||Accept any entry that appears to be the first episode of a series.||

=== Metadata filters ===

Filters based on content's metadata such as size and quality
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/content_size content_size]||Reject torrents and nzb's that do not meet size requirements.||
||[wiki:Plugins/quality quality]||Reject entries not of the specified quality.||

=== !FlexGet internal filters ===

Filters based on preexisting data or operations within !FlexGet
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugins/only_new only_new]||Causes all entries that were in the task on the previous run to be rejected at the input phase.||
||[wiki:Plugins/require_field require_field]||Reject entries that do not have the specified fields.||
||[wiki:Plugins/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugins/seen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugins/subtitle_queue subtitle_queue]||Add or accept files to get subtitles for.||

=== Torrent specific filters ===

Filters based specifically for torrents
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/content_filter content_filter]||Reject based on filenames within torrents.||
||[wiki:Plugins/magnets magnets]||Rejects entries with only magnet links.||
||[wiki:Plugins/private_torrents private_torrents]||Reject private or public torrents.||
||[wiki:Plugins/seen_info_hash seen_info_hash]||Rejects already downloaded torrents (detected by torrent info hash). [wiki:Builtin]||
||[wiki:Plugins/torrent_alive torrent_alive]||Reject any torrents that do not have an active tracker with seeds.||

=== Logical and operational filters ===

Filters that will accept/reject entries based on logical statements or simple file operations
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/accept_all accept_all]||Accept all entries.||
||[wiki:Plugins/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugins/exists_series exists_series]||Reject entries based on existing series in filesystem.||
||[wiki:Plugins/exists_movie exists_movie]||Reject entries based on existing movies in filesystem.||
||[wiki:Plugins/if if]||Filter based on simple python statements.||
||[wiki:Plugins/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugins/age age]||Reject, Accept entries based on age by looking at a date in a specified entry field.||

=== 3rd party sites filters ===

Filters based on data retrieved from 3rd party sites
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/crossmatch crossmatch]||Accept/reject based on other inputs (eg. imdb_list watchlist, ratings history).||
||[wiki:Plugins/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugins/imdb_required imdb_required]||Reject imdb incompatible entries.||
||[wiki:Plugins/rottentomatoes rottentomatoes]||Accept movie entries based on Rotten Tomatoes details.||


== Output ==

Execute operation(s) on accepted entries.

=== 3rd party software output ===

Send accepted entries to 3rd party software, usually downloaders.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/aria2 aria2]||Pass URIs to be downloaded to a local computer to the aria2 downloader.||
||[wiki:Plugins/deluge deluge]||Pass torrents directly to deluge bittorrent client, supporting magnet links.||
||[wiki:Plugins/nzbget nzbget]||Download nzbs with nzbget.||
||[wiki:Plugins/periscope periscope]||Download subtitles with Periscope.||
||[wiki:Plugins/pyload pyload]||http://pyload.org/.||
||[wiki:Plugins/qbittorrent qbittorrent]||Pass torrents directly to the qBittorrent client, supporting magnet links.||
||[wiki:Plugins/rtorrent rtorrent]||Pass torrents directly to rtorrent||
||[wiki:Plugins/rtorrent_magnet rtorrent_magnet]||Handles magnet URI's and produces rTorrent compatible torrent files (0.8.9+)||
||[wiki:Plugins/sabnzbd sabnzbd]||Download nzbs with SABnzbd.||
||[wiki:Plugins/subliminal subliminal]||Download subtitles with Subliminal.||
||[wiki:Plugins/transmission transmission]||Pass torrents directly to transmission, supporting magnet links.||
||[wiki:Plugins/utorrent utorrent]||Pass torrents directly to uTorrent.||
||[wiki:Plugins/uoccin_collection uoccin_collection_add]||`NEW` Mark all the accepted movies/episodes as collected in the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_collection uoccin_collection_remove]||`NEW` Unmark all the accepted movies/episodes as collected in the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_watched uoccin_watched_true]||`NEW` Mark all the accepted movies/episodes as watched in the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_watched uoccin_watched_false]||`NEW` Unmark all the accepted movies/episodes as watched in the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_watchlist uoccin_watchlist_add]||`NEW` Add all the accepted movies/series in the watchlist inside the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_watchlist uoccin_watchlist_remove]||`NEW` Remove all the accepted movies/series from the watchlist inside the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
||[wiki:Plugins/uoccin_subtitles uoccin_subtitles]||`NEW` Update the list of subtitles downloaded for the accepted movies/series in the [https://github.com/tarzasai/Uoccin Uoccin] data file.||

=== 3rd party sites output ===

Send accepted entries to 3rd party sites, usually for tracking purposes. 
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/myepisodes myepisodes]||Mark accepted episodes as acquired on !MyEpisodes.||
||[wiki:Plugins/thetvdb_add thetvdb_add]||Add accepted series to user's thetvdb.com favorites.||
||[wiki:Plugins/thetvdb_remove thetvdb_remove]||Remove accepted series from user's thetvdb.com favorites.||
||[wiki:Plugins/pogcal_acquired pogcal_acquired]||Mark accepted episodes on [http://pogdesign.co.uk/cat pogdesign TV calendar]||
||[wiki:Plugins/trakt_add trakt_add]||Add accepted episodes/movies to a list on trakt.tv.||
||[wiki:Plugins/trakt_remove trakt_remove]||Remove accepted episodes/movies from a list on trakt.tv.||
||[wiki:Plugins/kodi_library kodi_library]||Send clean/scan requests to a remote/local Kodi server.||

=== Notifier services output ===

Send accepted entries to notification services.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/email email]||Send email when new content is passed.||
||[wiki:Plugins/prowl prowl]||Send prowl notifications (iPhone).||
||[wiki:Plugins/pushover pushover]||`UPDATED` Send Pushover notifications (iPhone and Android).||
||[wiki:Plugins/rapidpush rapidpush]||An easy-to-use push notification service. (Android).||
||[wiki:Plugins/notify_osd notify_osd]||Send notifications to notify-osd.(linux only. Ubuntu tested)||
||[wiki:Plugins/notify_xmpp notify_xmpp]||Send notifications via XMPP.||
||[wiki:Plugins/notifymyandroid notifymyandroid]||Send notifications to android.||
||[wiki:Plugins/pushbullet pushbullet]||Send Pushbullet notifications (Android/iOS/Windows/Chrome Extension).||
||[wiki:Plugins/pushalot pushalot]||Send Pushalot notifications (Windows 8/Windows Phone).||
||[wiki:Plugins/sns sns]||Send SNS notifications.||
||[wiki:Plugins/slack slack]||Send Slack channel notifications.||

=== !FlexGet internal output ===

Use accepted entries as an input for various !FlexGet plugins such as add to movie queue, set series begin & etc.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/digest digest]||Collects entries from tasks to be combined into another task (usually for notification.)||
||[wiki:Plugins/movie_queue movie_queue]||`UPDATED` Add movies to movie queue.||
||[wiki:Plugins/set_series_begin set_series_begin]||Set the first episode to download for series.||

=== File operations output ===

Perform different file operations using accepted entries.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/copy copy]||Copy local files.||
||[wiki:Plugins/decompress decompress]||Extract Zip and RAR files.||
||[wiki:Plugins/delete delete]||Delete local files.||
||[wiki:Plugins/download download]||Download passed entries into given path.||
||[wiki:Plugins/exec exec]||Executes commands on entries.||
||[wiki:Plugins/ftp_download ftp_download]||Download entries retrieved from [wiki:Plugins/ftp_list ftp_list]||
||[wiki:Plugins/move move]||Move local files.||
||[wiki:Plugins/sftp_download sftp_download]||Download files from an SFTP server||
||[wiki:Plugins/sftp_upload sftp_upload]||Upload files to an SFTP server||

=== Generators output ===

Generate custom output using accepted entries
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/make_html make_html]||Generate HTML file from passed entries.||
||[wiki:Plugins/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugins/send_telegram send_telegram]||Send a Telegram message from passed entries.||

== Metadata plugins ==

Retrieve additional data from 3rd party sites. Used for population of more fields than default or to actively perform data retrieval for specific input types.
These are usually automatic ('''[wiki:Builtin]''') plugins which provide metainfo (fields) to '''[wiki:Entry]'''.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/imdb_lookup imdb_lookup]||Enable imdb parsing for imdb fields on-demand.||
||[wiki:Plugins/rottentomatoes_lookup rottentomatoes_lookup]||Enable Rotten Tomatoes parsing for Rotten Tomatoes fields on-demand.||
||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Fetch series information from http://thetvdb.com/||
||[wiki:Plugins/tmdb_lookup tmdb_lookup]||Enable http://www.themoviedb.org/ parsing for tmdb fields on-demand.||
||[wiki:Plugins/trakt_lookup trakt_lookup]||Enable http://trakt.tv/ parsing for trakt fields on-demand.||
||[wiki:Plugins/tvmaze_lookup tvmaze_lookup]||Enable http://tvmaze.com/ parsing for tvmaze fields on-demand.||
||[wiki:Plugins/check_subtitles check_subtitles]^1||Check subtitles presence for local files.||
||[wiki:Plugins/uoccin_lookup uoccin_lookup]||`NEW` Fetch all the supported information from the [https://github.com/tarzasai/Uoccin Uoccin] data file.||
^1. Not a builtin, configuration required to enable.^

== Modification plugins ==

Plugins that can manipulate data and perform various operations.

=== Request operations ===

Perform various operations on request that are being sent and received. 
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/cfscraper cfscraper]||Enables cloudflare scraping in a task.||
||[wiki:Plugins/cookies cookies]||Use FireFox3 cookies.||
||[wiki:Plugins/domain_delay domain_delay]||Sets a minimum interval between requests to specific domains.||
||[wiki:Plugins/formlogin formlogin]||Log in to web site via login form.||
||[wiki:Plugins/headers headers]||Modify HTTP headers.||
||[wiki:Plugins/proxy proxy]||Use a proxy to access resources.||
||[wiki:Plugins/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugins/urlrewrite_search urlrewrite_search]||Search for download URL from supported sites.||

=== File operations ===

Perform file oriented operations.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/extension extension]||Force a file extension.||
||[wiki:Plugins/free_space free_space]||Abort task when drive space is low.||
||[wiki:Plugins/path_by_ext path_by_ext]||Change (download) path based on file-type (extension).||
||[wiki:Plugins/path_select path_select]||Select a path based on disk stats||
||[wiki:Plugins/set set]||Set 'path' or other info per task. Can be dynamic per entry.||

=== Data operations ===

Manipulate relevant data based on input.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/assume_quality assume_quality]||Make assumptions about the qualities of releases.||
||[wiki:Plugins/add_trackers add_trackers]||Add trackers to torrents.||
||[wiki:Plugins/manipulate manipulate]||Allows regexp manipulation for entries.||
||[wiki:Plugins/parsing parsing]||Configure another parser for series and movie titles. (can help if IMDB/TMDB/TVDB lookup fails too often)||
||[wiki:Plugins/pathscrub pathscrub]||Cleans invalid characters from generated path/file names. (Used by other plugins that generate files.)||
||[wiki:Plugins/torrent_scrub torrent_scrub]||Removes non-standard keys like libtorrent resume information from downloads (which prevents the torrent from properly starting in Rtorrent).||
||[wiki:Plugins/urlrewrite urlrewrite]||User regexp for URL Rewriting.||

=== !FlexGet internal operations ===

Perform various !FlexGet operations.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/archive archive]||Archive all seen entries for searchable database for later retrieval.||
||[wiki:Plugins/delay delay]||Adds artificial delay into a task.||
||[wiki:Plugins/disable disable]||Disable builtin plugin(s) from a task, or plugins included from a template.||
||[wiki:Plugins/include include]||Include configuration from another yaml file.||
||[wiki:Plugins/interval interval]||Maintain minimum poll interval for the task.||
||[wiki:Plugins/manual manual]||Only run the task when explicitly specified.||
||[wiki:Plugins/no_entries_ok no_entries_ok]||Silence warnings about task not producing entries, for tasks where that is normal.||
||[wiki:Plugins/priority priority]||Change task execution order.||
||[wiki:Plugins/plugin_priority plugin_priority]||Change plugin priorities.||
||[wiki:Plugins/remember_rejected remember_rejected]||Remember rejections and reject them in future runs.||
||[wiki:Plugins/retry_failed retry_failed]||Save failed entries so they can be retried. [wiki:Builtin]||
||[wiki:Plugins/secrets secrets]||Replace specific jinja2 values in config before executing tasks.||
||[wiki:Plugins/sequence sequence]||Allows the same plugin to be configured multiple times in a task.||
||[wiki:Plugins/sleep sleep]||Causes a pause to occur at a specified point during task execution.||
||[wiki:Plugins/sort_by sort_by]||Sort entries in a task.||
||[wiki:Plugins/template template]||Provides global configuration and named templates.||
||[wiki:Plugins/verify_ssl_certificates verify_ssl_certificates]||Can turn off SSL certificate verification on a task.||
||[wiki:Plugins/version_checker version_checker]||Checks if user is running latest Flexget version on a given interval.||

=== 3rd party software ===

Perform operations on 3rd part software.
||'''Keyword'''||'''Description'''||
||[wiki:Plugins/clean_transmission clean_transmission]||Clean Transmission queue.||
||[wiki:Plugins/plugin_rutracker plugin_rutracker]||Supports downloading torrents from rutracker.||
||[wiki:Plugins/uoccin_reader uoccin_reader]||`NEW` Synchronize a [https://github.com/tarzasai/Uoccin Uoccin] data file.||

== Search ==

||[wiki:Plugins/search_rss search_rss]||Search with parametrized rss feed.||

== Daemon ==

These plugins are specifically for when !FlexGet is being used in daemon mode. They differ from the other plugins documented here, in that they should be configured at the root of your config. Not inside any tasks or templates.

||[wiki:Plugins/Daemon/scheduler scheduler]||Executes tasks with a given interval or schedule while daemon is running.||

== Command Line Interface ==

Use `flexget --help` for full list of subcommands. `--help` can also be used with any of the subcommands for further help text.

||[wiki:Plugins/cli/inject inject]||Inject entries into tasks from the CLI.||
||[wiki:Plugins/cli/service service]||'''{{{EXPERIMENTAL}}}''' A Windows service installer for the !FlexGet daemon.||

=== `execute` command options ===

Use `flexget execute --help` for full option list.

||[wiki:Plugins/--cli-config --cli-config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugins/--dump --dump]||Display all entries after task execution.||
||[wiki:Plugins/--tasks --tasks]||Executes only the specified task(s)||
||[wiki:Plugins/--inject --inject]||Injects custom entry into task(s).||
||[wiki:Plugins/try_regexp --try-regexp]||Test how regexps work on task(s) interactively.||

== Third-party plugin ==

Plugins can be installed by simply placing them in `~/.flexget/plugins/`

||[http://flexget.com/ticket/1435 jdownloader]||jDownloader output - perhaps included in the core package sooner or later.||
||[https://github.com/jawilson/dotfiles/blob/master/flexget/plugins/my_movie_filter.py my_movie_filter]||An extremely specific, no longer working, custom movie filter by jawilson.||