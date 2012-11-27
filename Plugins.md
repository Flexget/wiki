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

All configuration examples are assumed to be placed under a task. So if documentation has example:

{{{
series:
  - name
}}}

In full configuration this goes into:

{{{
tasks:
  task_name:
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
||[wiki:Plugins/discover discover]||Produce entries from search results.||
||[wiki:Plugins/emit_movie_queue emit_movie_queue]||'''{{{NEW}}}''' Emit your [wiki:Plugins/movie_queue movie_queue], useful for example with [wiki:Plugins/discover discover].||
||[wiki:Plugins/find find]||'''{{{NEW}}}''' Search through a local directory looking for files as a input.||
||[wiki:Plugins/from_deluge from_deluge]||'''{{{NEW}}}''' Use torrents loaded in a Deluge daemon as input.||
||[wiki:Plugins/from_transmission from_transmission]||'''{{{NEW}}}''' Use torrents loaded in Transmission as input.||
||[wiki:Plugins/html html]||Parse any HTML-page.||
||[wiki:Plugins/imdb_list imdb_list]||Use movies in your IMDb list as an input (eg. watchlist, rating history).||
||[wiki:Plugins/inputs inputs]||'''{{{NEW}}}''' Configure the same input plugin multiple times in one task.||
||[wiki:Plugins/listdir listdir]||Use any local directory listing as a input.||
||[wiki:Plugins/pogcal pogcal]||'''{{{NEW}}}''' Produce entries for shows marked on your [http://www.pogdesign.co.uk/cat/ pogdesign calendar].||
||[wiki:Plugins/rlslog rlslog]||Parse [http://rlslog.net] category.||
||[wiki:Plugins/rottentomatoes_list rottentomatoes_list]||Use movies from [http://www.rottentomatoes.com Rotten Tomatoes] lists.||
||[wiki:Plugins/rss rss]||Parse RSS-feed.||
||[wiki:Plugins/scenereleases scenereleases]||Parse [http://scenereleases.info].||
||[wiki:Plugins/tail tail]||Tail a log file (eg. irc logs)||
||[wiki:Plugins/text text]||Parse any text data||
||[wiki:Plugins/thetvdb_favorites thetvdb_favorites]||'''{{{NEW}}}''' Produce an entry for all shows you have marked as favorites at http://thetvdb.com.||
||[wiki:Plugins/trakt_list trakt_list]||'''{{{NEW}}}''' Create entries from one of your trakt.tv lists.||
||[wiki:Plugins/tvt tvt]||'''BROKEN''' Parse [http://tvtorrents.com].||

== Filters ==

Reject or Accept [wiki:Entry entries] based on given rules. A single task may have any number of filters.[[BR]]
If you plan to use multiple filters per task, you should look at [wiki:Filtering filtering operations] to understand how they work.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/accept_all accept_all]||Accept all entries.||
||[wiki:Plugins/all_series all_series]||'''{{{NEW}}}'''  Accepts any entry that appears to be an episode of a series.||
||[wiki:Plugins/content_filter content_filter]||'''{{{NEW}}}'''  Reject based on filenames within torrents.||
||[wiki:Plugins/content_size content_size]||'''{{{NEW}}}'''  Reject torrents and nzb's that do not meet size requirements.||
||[wiki:Plugins/crossmatch crossmatch]||'''{{{NEW}}}'''  Accept/reject based on other inputs (eg. imdb_list watchlist, ratings history).||
||[wiki:Plugins/exists exists]||Reject entries based on existing files in filesystem.||
||[wiki:Plugins/exists_series exists_series]||Reject entries based on existing series in filesystem.||
||[wiki:Plugins/exists_movie exists_movie]||Reject entries based on existing movies in filesystem.||
||[wiki:Plugins/if if]||'''{{{NEW}}}''' Filter based on simple python statements.||
||[wiki:Plugins/imdb imdb]||Accept movie entries based on imdb details.||
||[wiki:Plugins/imdb_required imdb_required]||Reject imdb incompatible entries.||
||[wiki:Plugins/limit_new limit_new]||Allow only given number of entries to pass per execution.||
||[wiki:Plugins/movie_queue movie_queue]||Accept movies from movie queue.||
||[wiki:Plugins/magnets magnets]||Rejects entries with only magnet links.||
||[wiki:Plugins/only_new only_new]||'''{{{NEW}}}'''  Causes all entries that were in the task on the previous run to be rejected at the input phase.||
||[wiki:Plugins/private_torrents private_torrents]||'''{{{NEW}}}'''  Reject private or public torrents.||
||[wiki:Plugins/proper_movies proper_movies]||'''{{{NEW}}}'''  Keep track of downloaded movies and force re-download proper versions.||
||[wiki:Plugins/quality quality]||Reject entries not of the specified quality.||
||[wiki:Plugins/regexp regexp]||Reject, Accept entries by using regular expression.||
||[wiki:Plugins/reject_failed reject_failed]||Reject entries that have failed too many times in the past. [wiki:Builtin]||
||[wiki:Plugins/require_field require_field]||'''{{{NEW}}}'''  Reject entries that do not have the specified fields.||
||[wiki:Plugins/rottentomatoes rottentomatoes]||'''{{{NEW}}}'''  Accept movie entries based on Rotten Tomatoes details.||
||[wiki:Plugins/seen_movies seen_movies]||Rejects already downloaded movies (detected by imdb-link).||
||[wiki:Plugins/seen_info_hash seen_info_hash]||Rejects already downloaded torrents (detected by torrent info hash). [wiki:Builtin]||
||[wiki:Plugins/seen seen]||Reject already downloaded entries. [wiki:Builtin]||
||[wiki:Plugins/series series]||Accept TV-series episodes. Quality and episode number aware.||
||[wiki:Plugins/series_premiere series_premiere]||'''{{{NEW}}}'''  Accept any entry that appears to be the first episode of a series.||
||[wiki:Plugins/torrent_alive torrent_alive]||'''{{{NEW}}}''' Reject any torrents that do not have an active tracker with seeds.||

== Site integration & Auto configuration ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/imdb_lookup imdb_lookup]||Enable imdb parsing for imdb fields on-demand.||
||[wiki:Plugins/myepisodes myepisodes]||'''{{{NEW}}}''' Mark accepted episodes as acquired on !MyEpisodes.||
||[wiki:Plugins/rottentomatoes_lookup rottentomatoes_lookup]||'''{{{NEW}}}''' Enable Rotten Tomatoes parsing for Rotten Tomatoes fields on-demand.||
||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Fetch series information from thetvdb.||
||[wiki:Plugins/tmdb_lookup tmdb_lookup]||'''{{{NEW}}}''' Enable http://www.themoviedb.org/ parsing for imdb fields on-demand.||
||[wiki:Plugins/trakt_acquired trakt_acquired]||'''{{{NEW}}}''' Mark accepted episodes/movies as acquired on trakt.tv.||

These plugins configure other plugins from external sources like 3rd party sites.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/import_series import_series]||'''{{{NEW}}}'''  Configures the series plugin with all the shows given by any input plugin (eg. listdir, rss). ||

== Outputs ==

Execute operation(s) on accepted entries.

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/deluge deluge]||Pass torrents directly to deluge bittorrent client.||
||[wiki:Plugins/download download]||Download passed entries into given path.||
||[wiki:Plugins/email email]||'''{{{UPDATED}}}''' Send email when new content is passed.||
||[wiki:Plugins/exec exec]||Executes commands on entries.||
||[wiki:Plugins/notifymyandroid notifymyandroid]||'''{{{NEW}}}'''  Send notifications to android.||
||[wiki:Plugins/make_html make_html]||Generate HTML file from passed entries.||
||[wiki:Plugins/make_rss make_rss]||Generate RSS-feed file from passed entries.||
||[wiki:Plugins/move move]||'''{{{NEW}}}''' Move local files.||
||[wiki:Plugins/prowl prowl]||Send prowl notifications (iPhone).||
||[wiki:Plugins/pushover pushover]||'''{{{NEW}}}''' Send Pushover notifications (iPhone and Android).||
||[wiki:Plugins/pyload pyload]||'''{{{NEW}}}'''  http://pyload.org/.||
||[wiki:Plugins/sabnzbd sabnzbd]||Download nzbs with SABnzbd.||
||[wiki:Plugins/transmission transmission]||Pass entries' url to transmission, supporting magnet links.||
||[wiki:Plugins/queue_movies queue_movies]||'''{{{NEW}}}'''  Add to movie queue.||

== Modify / Other ==

||'''Keyword'''||'''Description'''||
||[wiki:Plugins/add_trackers add_trackers]||Add trackers to torrents.||
||[wiki:Plugins/archive archive]||'''{{{UPGRADED}}}''' Archive all seen entries for searchable database for later retrieval.||
||[wiki:Plugins/cookies cookies]||'''{{{UPGRADED}}}''' Use FireFox3 cookies.||
||[wiki:Plugins/delay delay]||Adds artificial delay into a task.||
||[wiki:Plugins/disable_builtins disable_builtins]||Disable builtin plugin(s) from a task.||
||[wiki:Plugins/disable_plugin disable_plugin]||'''{{{NEW}}}''' Disable plugins from presets.||
||[wiki:Plugins/domain_delay domain_delay]||'''{{{NEW}}}''' Sets a minimum interval between requests to specific domains.||
||[wiki:Plugins/extension extension]||Force a file extension.||
||[wiki:Plugins/formlogin formlogin]||Log in to web site via login form.||
||[wiki:Plugins/free_space free_space]||Abort task when drive space is low.||
||[wiki:Plugins/headers headers]||Modify HTTP headers.||
||[wiki:Plugins/include include]||Include configuration from another yaml file.||
||[wiki:Plugins/interval interval]||Maintain minimum poll interval for the task.||
||[wiki:Plugins/manipulate manipulate]||'''{{{NEW}}}''' Allows regexp manipulation for entries.||
||[wiki:Plugins/manual manual]||'''{{{NEW}}}''' Only run the task when explicitly specified.||
||[wiki:Plugins/pathscrub pathscrub]||'''{{{NEW}}}''' Cleans invalid characters from generated path/file names. (Used by other plugins that generate files.)||
||[wiki:Plugins/path_by_ext path_by_ext]||Change (download) path based on file-type (extension).||
||[wiki:Plugins/priority priority]||Change task execution order.||
||[wiki:Plugins/proxy proxy]||'''{{{NEW}}}''' Use a proxy to access resources.||
||[wiki:Plugins/plugin_priority plugin_priority]||Change plugin priorities.||
||[wiki:Plugins/remove_trackers remove_trackers]||Remove trackers from a torrent.||
||[wiki:Plugins/preset preset]||Provides global configuration and named presets.||
||[wiki:Plugins/set set]||Set 'path' or other info per task. Can be dynamic per entry.||
||[wiki:Plugins/sleep sleep]||Causes a pause to occur before execution of a task.||
||[wiki:Plugins/sort_by sort_by]||Sort entries in a task.||
||[wiki:Plugins/torrent_scrub torrent_scrub]||Removes non-standard keys like libtorrent resume information from downloads (which prevents the torrent from properly starting in Rtorrent).||
||[wiki:Plugins/urlrewrite urlrewrite]||User regexp for URL Rewriting.||
||[wiki:Plugins/urlrewrite_search urlrewrite_search]||Search for download URL from supported sites.||
||[wiki:Plugins/verify_ssl_certificates verify_ssl_certificates]||Can turn off SSL certificate verification on a task.||

== Metainfo ==

These are usually automatic ([wiki:Builtin]) plugins which provide metainfo (fields) to [wiki:Entry].

||[wiki:Plugins/metainfo_quality metainfo_quality]||Parses quality from the entry.||
||[wiki:Plugins/metainfo_task metainfo_task]||Populates task field for entries.||
||[wiki:Plugins/metainfo_series metainfo_series]^1^||Populates series related fields for entries, even without [wiki:Plugins/series series] plugin.||
||[wiki:Plugins/metainfo_imdb metainfo_imdb]||Detects imdb urls from description.||

^1. Not a builtin, configuration required to enable.^

== Command line plugins ==

||[wiki:Plugins/--cli-config --cli-config]||Allow using values from commandline in YML-configuration file.||
||[wiki:Plugins/--dump --dump]||Display all entries after task execution.||
||[wiki:Plugins/--task --task]||Executes only the specified task(s)||
||[wiki:Plugins/--inject --inject]||Injects custom entry into task(s).||
||[wiki:Plugins/try_regexp --try-regexp]||Test how regexps work on task(s) interactively.||

== 3rd party plugins ==

Plugins can be installed by simply placing them in `~/.flexget/plugins/`

||[wiki:Plugins/rtorrent rtorrent]||'''{{{NEW}}}''' Scan (parts of) your rtorrent session.||
||[wiki:Plugins/rtorrent_magnet rtorrent_magnet]||'''{{{NEW}}}''' Handles magnet URI's and produces rTorrent compatible torrent files (0.8.9+)||
||[https://github.com/atlanta800/dotfiles/blob/master/flexget/plugins/my_movie_filter.py my_movie_filter]||'''{{{NEW}}}''' An extremely specific custom movie filter by atlanta800.||
||[https://github.com/nikdoof/flexget-twitter flexget-twitter]||'''{{{NEW}}}''' Twitter output plugin, allowing posting to twitter when entries are accepted.||
||[http://flexget.com/ticket/1435 jdownloader]||jDownloader output - perhaps included in the core package sooner or later.||