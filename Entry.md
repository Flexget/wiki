= Entry =

Entry represents a single item created by input(s), usually a downloadable content.
It contains all the information necessary for [wiki:Plugins plugins] to perform their job. Usually some [wiki:FilterOperations action for entry].

For example, the [wiki:Plugins/regexp regexp] plugin checks whether the given regular expression matches the entry's '''title''' or '''url''' and acts accordingly.

'''Example of an entry:'''

These are mandatory fields

||'''Name'''||'''Value'''||
||title||Some.Awesome.Series.S01E01.XviD-Foo||
||url||!http://site.com/download/Some.Awesome.Series.S01E01.XviD-Foo.torrent||

== Known fields ==

Entry ''may'' have any of these fields, but is not ''guaranteed'' to have any of them.

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
||imdb_year||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb year||
||imdb_score||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb score||
||imdb_votes||[wiki:Plugins/imdb_lookup imdb_lookup]*||Imdb votes||
||imdb_genres||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb genres||
||imdb_languages||[wiki:Plugins/imdb_lookup imdb_lookup]*||List of imdb languages||
||imdb_photo||[wiki:Plugins/imdb_lookup imdb_lookup]*||Url for photo (hotlinking prevented)||
||imdb_plot_outline||[wiki:Plugins/imdb_lookup imdb_lookup]*||Plot outline||
||imdb_actors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Actors dictionary (key: imdbid, value: name)||
||imdb_directors||[wiki:Plugins/imdb_lookup imdb_lookup]*||Actors dictionary (imdbid, name)||
||output||[wiki:Plugins/download download]||Downloaded file||
||torrent||modify_torrent||When entry is a torrent this contains [wiki:TorrentObject Torrent class]||
||data||[wiki:Plugins/download download]||Internal. Binary content.||
||content_size||[wiki:Plugins/content_size content_size]||Parsed size of torrents or NZBs.||
||location||[wiki:Plugins/listdir listdir]||The local filename of the entry.||
||series_name_tvdb||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series name provided by thetvdb||
||series_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series rating||
||series_status||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series status(Continuing or Ended)||
||series_runtime||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series runtime in minutes)||
||series_first_air_date||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series premier date||
||series_air_time||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series air time||
||series_content_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series content ration||
||series_genres||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series genres||
||series_network||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series network||
||series_banner_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series banenr url||
||series_fanart_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series fanart url||
||series_poster_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series poster url||
||series_airs_day_of_week||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series airs date of the week||
||series_actors||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series actors||
||series_language||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series language(en, fr, etc.)||
||imdb_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Series imdb url||
||zap2it_id||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||||
||ep_name||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode name||
||ep_overview||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode plot||
||ep_director||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode director||
||ep_writer||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode writer||
||ep_air_date||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode air date||
||ep_rating||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode rating||
||ep_guest_stars||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode guest stars||
||ep_image_url||[wiki:Plugins/thetvdb_lookup thetvdb_lookup]||Episode image url||

^* = and other plugins that utilize this plugin^
