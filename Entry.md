= Entry =

Entry represents a single item created by input(s), usually a downloadable content.
It contains all the information necessary for [wiki:Plugins plugins] to perform their job (usually some [wiki:FilterOperations operation] on the entry).

For example, the [wiki:Plugins/regexp regexp] plugin checks whether the given regular expression matches the entry's '''title''' or '''url''' and acts accordingly.

'''Example of an entry:'''

These are mandatory fields

||'''Name'''||'''Value'''||
||title||Some.Awesome.Series.S01E01.XviD-Foo||
||url||!http://site.com/download/Some.Awesome.Series.S01E01.XviD-Foo.torrent||

== Known fields ==

Entry ''may'' have any of these fields, but is not ''guaranteed'' to have any of them. It may have other fields as well depending on configuration. Use {{{--dump}}} option to see your task content.

||'''Name'''||'''Created by'''||'''Description'''||
||path||multiple plugins||Path where this entry content should be saved||
||description||[wiki:Plugins/rss rss]||Item description||
||rss_pubdate||[wiki:Plugins/rss rss]||Date the RSS item was published||
||task||metainfo_task||Task name which this entry belongs to||
||quality||metainfo_quality, [wiki:Plugins/series series]||Detected quality, ie. `720p`||
||series_name||[wiki:Plugins/series series], metainfo_series||Series name||
||series_season||[wiki:Plugins/series series], metainfo_series||Series season||
||series_episode||[wiki:Plugins/series series], metainfo_series||Series episode||
||series_id||[wiki:Plugins/series series]||Series episode identifier, ie. `S01E02` or `2009-12-1`||
||series_date||[wiki:Plugins/series series]||The date of the episode. (only available for date based series)||
||proper||[wiki:Plugins/series series]||Whether this entry is a proper or repack release||
||imdb_url||[wiki:Plugins/imdb_lookup imdb_lookup]+others||Imdb url||
||imdb_id||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb identifier||
||imdb_name||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb name||
||imdb_original_name||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb original name||
||imdb_year||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb year||
||imdb_score||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb score||
||imdb_votes||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb votes||
||imdb_genres||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb genres||
||imdb_languages||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb languages||
||imdb_photo||[wiki:Plugins/imdb_lookup imdb_lookup]*||Url for photo (hotlinking prevented)||
||imdb_plot_outline||[wiki:Plugins/imdb_lookup imdb_lookup]*||Plot outline||
||imdb_actors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Actors dictionary (key: imdbid, value: name)||
||imdb_directors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Directors dictionary (imdbid, name)||
||movie_name||[wiki:Plugins/imdb_lookup imdb_lookup]*||Movie title||
||movie_year||[wiki:Plugins/imdb_lookup imdb_lookup]*||Movie release year||
||output||[wiki:Plugins/download download]||Downloaded file||
||torrent||modify_torrent||When entry is a torrent this contains [wiki:TorrentObject Torrent class]||
||data||[wiki:Plugins/download download]||Internal. Binary content.||
||content_size||[wiki:Plugins/content_size content_size]||Parsed size of torrents or NZBs.||
||location||[wiki:Plugins/filesystem filesystem]||The local filename of the entry.||
||timestamp||[wiki:Plugins/find find]||The local file update time of the entry.||
||subtitles||[wiki:Plugins/check_subtitles check_subtitles]||A list of languages about subtitles founds on disk (local files only)||
||plex_server||[wiki:Plugins/plex plex]||If set, PMS hostname. Otherwise PMS IP.||
||plex_server_ip||[wiki:Plugins/plex plex]||PMS IP.||
||plex_port||[wiki:Plugins/plex plex]||PMS port.||
||plex_section||[wiki:Plugins/plex plex]||Section number.||
||plex_section_name||[wiki:Plugins/plex plex]||Section name.||
||plex_path||[wiki:Plugins/plex plex]||Entry path on PMS.||
||plex_duration||[wiki:Plugins/plex plex]||Entry length in seconds.||
||plex_thumb||[wiki:Plugins/plex plex]||Episode thumbnail, series only.||
||plex_art||[wiki:Plugins/plex plex]||Series or movie art as configured in PMS||
||plex_cover||[wiki:Plugins/plex plex]||Series cover for series, movie cover for movies.||
||plex_season_cover||[wiki:Plugins/plex plex]||Season cover, series only. If used in movies, movie cover will be set.||
||plex_title||[wiki:Plugins/plex plex]||Episode name as indexed on PMS.||
||plex_summary||[wiki:Plugins/plex plex]||Entry summary.||
||plex_status||[wiki:Plugins/plex plex]||Entry status: seen, inprogress or unwatched.||
||plex_url||[wiki:Plugins/plex plex]||Original plex url.||
||tvdb_series_name||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series name provided by thetvdb||
||tvdb_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series rating||
||tvdb_status||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series status(Continuing or Ended)||
||tvdb_runtime||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series runtime in minutes)||
||tvdb_first_air_date||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series premier date||
||tvdb_air_time||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series air time||
||tvdb_content_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series content ration||
||tvdb_genres||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series genres||
||tvdb_network||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series network||
||tvdb_banner_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series banner url||
||tvdb_fanart_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series fanart url||
||tvdb_poster_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series poster url||
||tvdb_airs_day_of_week||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series airs date of the week||
||tvdb_actors||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||List of series actors||
||tvdb_language||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series language(en, fr, etc.)||
||imdb_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series imdb url||
||zap2it_id||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||||
||tvdb_ep_name||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode name||
||tvdb_ep_overview||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode plot||
||tvdb_ep_directors||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||List of episode directors||
||tvdb_ep_writers||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||List of episode writers||
||tvdb_ep_air_date||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode air date||
||tvdb_ep_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode rating||
||tvdb_ep_guest_stars||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||List of episode guest stars||
||tvdb_ep_image_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode image url||
||trakt_series_name||[wiki:Plugins/trakt_lookup trakt_lookup]||Series name provided by trakt||
||trakt_series_runtime||[wiki:Plugins/trakt_lookup trakt_lookup]||Series runtime in minutes||
||trakt_series_first_aired_epoch||[wiki:Plugins/trakt_lookup trakt_lookup]||Series premier data in epoch time||
||trakt_series_first_aired_iso||[wiki:Plugins/trakt_lookup trakt_lookup]||Time stamp of premier date||
||trakt_series_air_time||[wiki:Plugins/trakt_lookup trakt_lookup]||Time the series ran||
||trakt_series_content_rating||[wiki:Plugins/trakt_lookup trakt_lookup]||Content rating ex: TV-14||
||trakt_series_genres||[wiki:Plugins/trakt_lookup trakt_lookup]||Series genres||
||trakt_series_netowrk||[wiki:Plugins/trakt_lookup trakt_lookup]||Series network||
||trakt_series_banner_url||[wiki:Plugins/trakt_lookup trakt_lookup]||Series banner||
||trakt_series_fanart_url||[wiki:Plugins/trakt_lookup trakt_lookup]||Series Fanart||
||trakt_series_poster_url||[wiki:Plugins/trakt_lookup trakt_lookup]||Series poster||
||trakt_series_imdb_id||[wiki:Plugins/trakt_lookup trakt_lookup]||Series IMDB ID||
||trakt_series_tvdb_id||[wiki:Plugins/trakt_lookup trakt_lookup]||Series TVDB ID||
||trakt_series_tvrage_id||[wiki:Plugins/trakt_lookup trakt_lookup]||Series TVRage ID||
||trakt_series_actors||[wiki:Plugins/trakt_lookup trakt_lookup]||Series actors||
||trakt_series_country||[wiki:Plugins/trakt_lookup trakt_lookup]||Production Country||
||trakt_series_year||[wiki:Plugins/trakt_lookup trakt_lookup]||Series release year||
||trakt_series_status||[wiki:Plugins/trakt_lookup trakt_lookup]||Series status(ex: Airing)||
||trakt_series_overview||[wiki:Plugins/trakt_lookup trakt_lookup]||Series overview||
||trakt_ep_name||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode name||
||trakt_ep_first_aired_epoch||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode premier date in epoch||
||trakt_ep_first_aired_iso||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode premier date time stamp||
||trakt_ep_image_url||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode screenshot||
||trakt_ep_overview||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode overview||
||trakt_season||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode season||
||trakt_episode||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode Number||
||trakt_ep_id||[wiki:Plugins/trakt_lookup trakt_lookup]||Episode id string 'S01E01'||
||trakt_ep_tvdb_id||[wiki:Plugins/trakt_lookup trakt_lookup]||TVDB ID of episode||
||trakt_watched||[wiki:Plugins/trakt_watched_lookup trakt_watched_lookup]||Episode marked seen (true/false)||

^* = and other plugins that utilize this plugin^