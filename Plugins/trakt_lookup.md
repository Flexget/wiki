= Trakt.tv Series Lookup =

This plugin returns series information from Trakt.tv. The name of the series usually has to be VERY close to what's shown on Trakt.[[BR]]
If you are having problems returning the correct information for a show. Please add to the series the tvdb_id using the [wiki:Plugins/set set] command.[[BR]]

----

{{{
series:
  - some_series:
      set:
        tvdb_id: <tvdb_id>
}}}

This plugin populates fields on entries that have been identified as series by !Flexget. They may also be used in other plugins "ex:[wiki:Plugins/make_rss make_rss]"
----
'''Series Metainfo'''

||trakt_series_name||Series name provided by trakt||
||trakt_series_runtime||Series runtime in minutes||
||trakt_series_first_aired_epoch||Series premier data in epoch time||
||trakt_series_first_aired_iso||Time stamp of premier date||
||trakt_series_air_time||Time the series ran||
||trakt_series_content_rating||Content rating ex: TV-14||
||trakt_series_genres||Series genres||
||trakt_series_netowrk||Series network||
||trakt_series_banner_url||Series banner||
||trakt_series_fanart_url||Series Fanart||
||trakt_series_poster_url||Series poster||
||trakt_series_imdb_id||Series IMDB ID||
||trakt_series_tvdb_id||Series TVDB ID||
||trakt_series_tvrage_id||Series TVRage ID||
||trakt_series_actors||Series actors||
||trakt_series_country||Production Country||
||trakt_series_year||Series release year||
||trakt_series_status||Series status(ex: Airing)||
||trakt_series_overview||Series overview||
||imdb_url||IMDB url for linking||
[[BR]]
----
[[BR]]
'''Episode Metainfo'''

||trakt_ep_name||Episode name||
||trakt_ep_first_aired_epoch||Episode premier date in epoch||
||trakt_ep_first_aired_iso||Episode premier date time stamp||
||trakt_ep_image_url||Episode screenshot||
||trakt_ep_overview||Episode overview||
||trakt_season||Episode season||
||trakt_episode||Episode Number||
||trakt_ep_id||Episode id string 'S01E01'||
||trakt_ep_tvdb_id||TVDB ID of episode||
----
[[BR]]
----
'''Example'''[[BR]]

The most common uses we'll see are using it for [wiki:Plugins/make_rss make_rss] and making pretty filenames using [wiki:Plugins/set set] to set {{{content_filename}}} in the [wiki:Plugins/deluge deluge]. The 'default' jinja filter is used to insert 'Unknown' if trakt_lookup failes to get an entry field.
{{{
trakt_lookup: yes
set:
  content_filename: "{{series_name}} - {{series_id}} - {{trakt_ep_name|default('Unknown')}}"
}}}