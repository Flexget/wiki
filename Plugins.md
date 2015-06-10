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

All configuration examples are assumed to be placed under a task. So if documentation has this example:

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

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/apple_trailers apple_trailers]||Get movie trailers from Apple.com||
||[wiki:Plugins/betaseries_list betaseries_list]||Use series you follow on www.betaseries.com as an input||
||[wiki:Plugins/csv csv]||Parse any CSV-file||
||[wiki:Plugins/couchpotato couchpotato]||'''{{{UPDATED}}}''' Produce entries from couchpotato wanted list||
||[wiki:Plugins/discover discover]||'''{{{UPDATED}}}''' Produce entries from search results.||
||[wiki:Plugins/emit_digest emit_digest]||'''{{{NEW}}}''' Outputs entries which have been collected by the [wiki:Plugins/digest digest] plugin.||
||[wiki:Plugins/emit_movie_queue emit_movie_queue]||Emit your [wiki:Plugins/movie_queue movie_queue], useful for example with [wiki:Plugins/discover discover].||
||[wiki:Plugins/emit_series emit_series]||'''{{{NEW}}}''' Emit the next episode needed for each series configured in the series plugin. Useful for example with [wiki:Plugins/discover discover].||
||[wiki:Plugins/find find]||Search through a local directory looking for files as a input.||
||[wiki:Plugins/from_deluge from_deluge]||Use torrents loaded in a Deluge daemon as input.||
||[wiki:Plugins/rtorrent from_rtorrent]||'''{{{NEW}}}'''Use torrents loaded in a rTorrent as input.||
||[wiki:Plugins/from_transmission from_transmission]||Use torrents loaded in Transmission as input.||
||[wiki:Plugins/html html]||Parse any HTML-page.||
||[wiki:Plugins/imdb_list imdb_list]||Use movies in your IMDb list as an input (eg. watchlist, rating history).||
||[wiki:Plugins/inputs inputs]||Configure the same input plugin multiple times in one task.||
||[wiki:Plugins/listdir listdir]||Use any local directory listing as a input.||
||[wiki:Plugins/plex plex]||'''{{{NEW}}}''' Produce entries for shows present in a [http://www.plexapp.com Plex Media Server] section.||
||[wiki:Plugins/pogcal pogcal]||'''{{{NEW}}}''' Produce entries for shows marked on your [http://www.pogdesign.co.uk/cat/ pogdesign calendar].||
||[wiki:Plugins/rlslog rlslog]||Parse [http://rlslog.net] category.||
||[wiki:Plugins/rottentomatoes_list rottentomatoes_list]||Use movies from [http://www.rottentomatoes.com Rotten Tomatoes] lists.||
||[wiki:Plugins/rss rss]||Parse RSS-feed.||
||[wiki:Plugins/sceper sceper]||Parse [http://sceper.ws].||
||[wiki:Plugins/sftp_list sftp_list]||'''{{{NEW}}}''' List files from an SFTP server||
||[wiki:Plugins/sickbeard sickbeard]||'''{{{UPDATED}}}''' Produce entries from Sickbeard's show list||
||[wiki:Plugins/sonarr sonarr]||'''{{{UPDATED}}}''' Produce entries from Sonarr's show list||
||[wiki:Plugins/tail tail]||Tail a log file (eg. irc logs)||
||[wiki:Plugins/text text]||Parse any text data||
||[wiki:Plugins/thetvdb_favorites thetvdb_favorites]||Produce an entry for all shows you have marked as favorites at http://thetvdb.com.||
||[wiki:Plugins/trakt_emit trakt_emit]||'''{{{NEW}}}''' Create entries for the latest or the next episode to watch or collect by your trakt.tv activity.||
||[wiki:Plugins/trakt_list trakt_list]||'''{{{NEW}}}''' Create entries from one of your trakt.tv lists.||
||[wiki:Plugins/transmission_files transmission_files]||'''{{{NEW}}}'''Use the contents of torrents loaded in Transmission as input.||
||[wiki:Plugins/twitterfeed twitterfeed]||'''{{{NEW}}}''' Create entries from a twitter account.||
||[wiki:Plugins/regexp_parse regexp_parse]||Use regular expressions to parse text from a web resource or file||
||[wiki:Plugins/ftp_list ftp_list]||'''{{{NEW}}}''' Lists the content of a remote FTP server||
||[wiki:Plugins/whatcd whatcd]||'''{{{NEW}}}''' Produce entries for content on [https://what.cd]||

== Filters ==

Reject or Accept '''[wiki:Entry entries]''' based on given rules. A single task may have any number of filters.[[BR]]
If you plan to use multiple filters per task, you should look at '''[wiki:Filtering filtering operations]''' to understand how they work.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/accept_all accept_all]||Accept all entries.||
||[wiki:Plugins/all_series all_series]||Accepts any entry that appears to be an episode of a series.||
||[wiki:Plugins/content_filter content_filter]||Reject based on filenames within torrents.||
||[wiki:Plugins/content_size content_size]||Reject torrents and nzb's that do not meet size requirements.||
||[wiki:Plugins/crossmatch crossmatch]||Accept/reject based on other inputs (eg. imdb_list watchlist, ratings history).||
||[wiki:Plugins/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugins/exists_series exists_series]||Reject entries based on existing series in filesystem.||
||[wiki:Plugins/exists_movie exists_movie]||Reject entries based on existing movies in filesystem.||
||[wiki:Plugins/if if]||Filter based on simple python statements.||
||[wiki:Plugins/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugins/imdb_required imdb_required]||Reject imdb incompatible entries.||
||[wiki:Plugins/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugins/movie_queue movie_queue]||Accept movies from movie queue.||
||[wiki:Plugins/magnets magnets]||Rejects entries with only magnet links.||
||[wiki:Plugins/only_new only_new]||Causes all entries that were in the task on the previous run to be rejected at the input phase.||
||[wiki:Plugins/private_torrents private_torrents]||Reject private or public torrents.||
||[wiki:Plugins/proper_movies proper_movies]||Keep track of downloaded movies and force re-download proper versions.||
||[wiki:Plugins/quality quality]||Reject entries not of the specified quality.||
||[wiki:Plugins/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugins/require_field require_field]||Reject entries that do not have the specified fields.||
||[wiki:Plugins/rottentomatoes rottentomatoes]||Accept movie entries based on Rotten Tomatoes details.||
||[wiki:Plugins/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugins/seen_info_hash seen_info_hash]||Rejects already downloaded torrents (detected by torrent info hash). [wiki:Builtin]||
||[wiki:Plugins/seen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugins/series series]||Accept TV-series episodes. Quality and episode number aware.||
||[wiki:Plugins/series_premiere series_premiere]||Accept any entry that appears to be the first episode of a series.||
||[wiki:Plugins/subtitle_queue subtitle_queue]||'''{{{NEW}}}''' Add or accept files to get subtitles for.||
||[wiki:Plugins/torrent_alive torrent_alive]||Reject any torrents that do not have an active tracker with seeds.||

== Site integration & Auto configuration ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/imdb_lookup imdb_lookup]||Enable imdb parsing for imdb fields on-demand.||
||[wiki:Plugins/myepisodes myepisodes]||'''{{{NEW}}}''' Mark accepted episodes as acquired on !MyEpisodes.||
||[wiki:Plugins/pogcal_acquired pogcal_acquired]||'''{{{NEW}}}''' Mark accepted episodes on [http://pogdesign.co.uk/cat pogdesign TV calendar]||
||[wiki:Plugins/rottentomatoes_lookup rottentomatoes_lookup]||Enable Rotten Tomatoes parsing for Rotten Tomatoes fields on-demand.||
||[wiki:Plugins/thetvdb_add thetvdb_add]||'''{{{NEW}}}''' Add accepted series to user's thetvdb.com favorites.||
||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Fetch series information from thetvdb.||
||[wiki:Plugins/thetvdb_remove thetvdb_remove]||'''{{{NEW}}}''' Remove accepted series from user's thetvdb.com favorites.||
||[wiki:Plugins/tmdb_lookup tmdb_lookup]||Enable http://www.themoviedb.org/ parsing for tmdb fields on-demand.||
||[wiki:Plugins/trakt_add trakt_add]||Add accepted episodes/movies to a list on trakt.tv.||
||[wiki:Plugins/trakt_lookup trakt_lookup]||Enable series information from trakt.tv||
||[wiki:Plugins/trakt_remove trakt_remove]||Remove accepted episodes/movies from a list on trakt.tv.||

These plugins configure other plugins from external sources like 3rd party sites.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/configure_series configure_series]||Configures the series plugin with all the shows given by any input plugin (eg. listdir, rss). ||

== Outputs ==

Execute operation(s) on accepted entries.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/aria2 aria2]||Pass URIs to be downloaded to a local computer to the aria2 downloader.||
||[wiki:Plugins/copy copy]||Copy local files.||
||[wiki:Plugins/decompress decompress]||'''{{{NEW}}}''' Extract Zip and RAR files.||
||[wiki:Plugins/delete delete]||Delete local files.||
||[wiki:Plugins/deluge deluge]||Pass torrents directly to deluge bittorrent client, supporting magnet links.||
||[wiki:Plugins/digest digest]||'''{{{NEW}}}''' Collects entries from tasks to be combined into another task (usually for notification.)||
||[wiki:Plugins/download download]||Download passed entries into given path.||
||[wiki:Plugins/exec exec]||Executes commands on entries.||
||[wiki:Plugins/ftp_download ftp_download]||'''{{{NEW}}}''' Download entries retrieved from [wiki:Plugins/ftp_list ftp_list]||
||[wiki:Plugins/make_html make_html]||Generate HTML file from passed entries.||
||[wiki:Plugins/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugins/move move]||Move local files.||
||[wiki:Plugins/nzbget nzbget]||'''{{{NEW}}}''' Download nzbs with nzbget.||
||[wiki:Plugins/periscope periscope]||'''{{{NEW}}}''' Download subtitles with Periscope.||
||[wiki:Plugins/pyload pyload]||'''{{{NEW}}}'''  http://pyload.org/.||
||[wiki:Plugins/queue_movies queue_movies]||'''{{{Deprecated}}}''' Add to movie queue.||
||[wiki:Plugins/rtorrent rtorrent]||'''{{{NEW}}}'''Pass torrents directly to rtorrent||
||[wiki:Plugins/rtorrent_magnet rtorrent_magnet]||'''{{{NEW}}}''' Handles magnet URI's and produces rTorrent compatible torrent files (0.8.9+)||
||[wiki:Plugins/sabnzbd sabnzbd]||Download nzbs with SABnzbd.||
||[wiki:Plugins/sftp_download sftp_download]||'''{{{NEW}}}''' Download files from an SFTP server||
||[wiki:Plugins/set_series_begin set_series_begin]||'''{{{NEW}}}''' Set the first episode to download for series.||
||[wiki:Plugins/subliminal subliminal]||'''{{{NEW}}}''' Download subtitles with Subliminal.||
||[wiki:Plugins/transmission transmission]||Pass torrents directly to transmission, supporting magnet links.||
||[wiki:Plugins/utorrent utorrent]||'''{{{NEW}}}''' Pass torrents directly to uTorrent.||


== Outputs (notification) ==

||[wiki:Plugins/email email]||Send email when new content is passed.||
||[wiki:Plugins/prowl prowl]||Send prowl notifications (iPhone).||
||[wiki:Plugins/pushover pushover]||Send Pushover notifications (iPhone and Android).||
||[wiki:Plugins/rapidpush rapidpush]||An easy-to-use push notification service. (Android).||
||[wiki:Plugins/notify_osd notify_osd]||Send notifications to notify-osd.(linux only. Ubuntu tested)||
||[wiki:Plugins/notify_xmpp notify_xmpp]||'''{{{NEW}}}''' Send notifications via XMPP.||
||[wiki:Plugins/notifymyandroid notifymyandroid]||Send notifications to android.||
||[wiki:Plugins/pushbullet pushbullet]||Send Pushbullet notifications (Android/iOS/Windows/Chrome Extension).||
||[wiki:Plugins/pushalot pushalot]||'''{{{NEW}}}''' Send Pushalot notifications (Windows 8/Windows Phone).||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/add_trackers add_trackers]||Add trackers to torrents.||
||[wiki:Plugins/archive archive]||'''{{{UPGRADED}}}''' Archive all seen entries for searchable database for later retrieval.||
||[wiki:Plugins/assume_quality assume_quality]||'''{{{NEW}}}''' Make assumptions about the qualities of releases.||
||[wiki:Plugins/clean_transmission clean_transmission]||'''{{{NEW}}}''' Clean Transmission queue.||
||[wiki:Plugins/cookies cookies]||'''{{{UPGRADED}}}''' Use FireFox3 cookies.||
||[wiki:Plugins/delay delay]||Adds artificial delay into a task.||
||[wiki:Plugins/disable disable]||Disable builtin plugin(s) from a task, or plugins included from a template.||
||[wiki:Plugins/domain_delay domain_delay]||'''{{{NEW}}}''' Sets a minimum interval between requests to specific domains.||
||[wiki:Plugins/extension extension]||Force a file extension.||
||[wiki:Plugins/formlogin formlogin]||Log in to web site via login form.||
||[wiki:Plugins/free_space free_space]||Abort task when drive space is low.||
||[wiki:Plugins/headers headers]||Modify HTTP headers.||
||[wiki:Plugins/include include]||Include configuration from another yaml file.||
||[wiki:Plugins/interval interval]||Maintain minimum poll interval for the task.||
||[wiki:Plugins/manipulate manipulate]||Allows regexp manipulation for entries.||
||[wiki:Plugins/manual manual]||'''{{{NEW}}}''' Only run the task when explicitly specified.||
||[wiki:Plugins/no_entries_ok no_entries_ok]||Silence warnings about task not producing entries, for tasks where that is normal.||
||[wiki:Plugins/parsing parsing]||'''{{{NEW}}}'''Configure another parser for series and movie titles. (can help if IMDB/TMDB/TVDB lookup fails too often)||
||[wiki:Plugins/pathscrub pathscrub]||'''{{{NEW}}}''' Cleans invalid characters from generated path/file names. (Used by other plugins that generate files.)||
||[wiki:Plugins/path_by_ext path_by_ext]||Change (download) path based on file-type (extension).||
||[wiki:Plugins/path_select path_select]||'''{{{NEW}}}'''Select a path based on disk stats||
||[wiki:Plugins/priority priority]||Change task execution order.||
||[wiki:Plugins/proxy proxy]||'''{{{NEW}}}''' Use a proxy to access resources.||
||[wiki:Plugins/plugin_priority plugin_priority]||Change plugin priorities.||
||[wiki:Plugins/plugin_rutracker plugin_rutracker]||Supports downloadin torrents from rutracker.||
||[wiki:Plugins/remember_rejected remember_rejected]||Remember rejections and reject them in future runs.||
||[wiki:Plugins/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugins/retry_failed retry_failed]||Save failed entries so they can be retried. [wiki:Builtin]||
||[wiki:Plugins/secrets secrets]||'''{{{NEW}}}''' Replace specific jinja2 values in config before executing tasks.||
||[wiki:Plugins/sequence sequence]||Allows the same plugin to be configured multiple times in a task.||
||[wiki:Plugins/set set]||Set 'path' or other info per task. Can be dynamic per entry.||
||[wiki:Plugins/sleep sleep]||Causes a pause to occur at a specified point during task execution.||
||[wiki:Plugins/sort_by sort_by]||Sort entries in a task.||
||[wiki:Plugins/template template]||Provides global configuration and named templates.||
||[wiki:Plugins/torrent_scrub torrent_scrub]||Removes non-standard keys like libtorrent resume information from downloads (which prevents the torrent from properly starting in Rtorrent).||
||[wiki:Plugins/urlrewrite urlrewrite]||User regexp for URL Rewriting.||
||[wiki:Plugins/urlrewrite_search urlrewrite_search]||Search for download URL from supported sites.||
||[wiki:Plugins/verify_ssl_certificates verify_ssl_certificates]||Can turn off SSL certificate verification on a task.||

== Metainfo ==

These are usually automatic ('''[wiki:Builtin]''') plugins which provide metainfo (fields) to '''[wiki:Entry]'''.

||[wiki:Plugins/check_subtitles check_subtitles]||Check subtitles presence for local files.||
||[wiki:Plugins/metainfo_quality metainfo_quality]||Parses quality from the entry.||
||[wiki:Plugins/metainfo_task metainfo_task]||Populates task field for entries.||
||[wiki:Plugins/metainfo_series metainfo_series]^1^||Populates series related fields for entries, even without [wiki:Plugins/series series] plugin.||
||[wiki:Plugins/metainfo_imdb metainfo_imdb]||Detects imdb urls from description.||
||[wiki:Plugins/trakt_collected_lookup trakt_collected_lookup]||'''{{{NEW}}}''' Enable episodes collected status from trakt.tv user activity||
||[wiki:Plugins/trakt_watched_lookup trakt_watched_lookup]||'''{{{NEW}}}''' Enable episodes watched status from trakt.tv user activity||
^1. Not a builtin, configuration required to enable.^

== Search ==

||[wiki:Plugins/search_rss search_rss]||Search with parametrized rss feed.||

== Daemon ==

These plugins are specifically for when !FlexGet is being used in daemon mode. They differ from the other plugins documented here, in that they should be configured at the root of your config. Not inside any tasks or templates.

||[wiki:Plugins/Daemon/scheduler scheduler]||Executes tasks with a given interval or schedule while daemon is running.||

== Command line plugins for `execute` command ==

||[wiki:Plugins/--cli-config --cli-config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugins/--dump --dump]||Display all entries after task execution.||
||[wiki:Plugins/--tasks --tasks]||Executes only the specified task(s)||
||[wiki:Plugins/--inject --inject]||Injects custom entry into task(s).||
||[wiki:Plugins/try_regexp --try-regexp]||Test how regexps work on task(s) interactively.||

== Third-party plugins ==

Plugins can be installed by simply placing them in `~/.flexget/plugins/`

||[https://github.com/atlanta800/dotfiles/blob/master/flexget/plugins/my_movie_filter.py my_movie_filter]||An extremely specific custom movie filter by atlanta800.||
||[https://github.com/nikdoof/flexget-twitter flexget-twitter]||'''{{{NEW}}}''' Twitter output plugin, allowing posting to twitter when entries are accepted.||
||[http://flexget.com/ticket/1435 jdownloader]||jDownloader output - perhaps included in the core package sooner or later.||