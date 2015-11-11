= Trakt.tv Series Lookup =
**//Updated as of November 11th 2015. This plugin uses the new Trakt v2 API.//**

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
||trakt_series_year||Series release year||
||imdb_id||Series IMDB ID||
||tvdb_id||Series TVDB ID||
||tmdb_id||Series TMDB ID||
||trakt_show_id||Series Trakt.tv ID||
||trakt_series_tvrage_id||Series TVRage ID||
||trakt_series_slug||Series Trakt.tv slug eg. `the-matrix`||
||trakt_series_runtime||Series runtime in minutes||
||trakt_series_air_time||Time the series ran/runs||
||trakt_series_air_day||Day the series ran/runs||
||trakt_series_content_rating||Content rating ex: TV-14||
||trakt_series_genres||Series genres||
||trakt_series_network||Series network||
||imdb_url||IMDB url for linking||
||trakt_series_country||Series country origin||
||trakt_series_status||Series status ie. `returning series` (airing right now), `in production` (airing soon), `planned` (in development), `canceled` or `ended`||
||trakt_series_overview||Series overview/description||
||trakt_series_rating||Series rating on Trakt.tv eg. 8/10||
||trakt_series_aired_episodes||Number of aired episodes||
||trakt_series_episodes||List of episode titles||
||trakt_series_actors||Series actors||
----
'''Episode Metainfo'''

||trakt_ep_name||Episode name||
||trakt_ep_tvdb_id||TVDB ID of episode||
||trakt_ep_imdb_id||IMDb ID of episode||
||trakt_ep_tmdb_id||TMDB ID of episode||
||trakt_ep_tvrage_id||TVRage ID of episode||
||trakt_ep_first_aired||Episode premier date||
||trakt_ep_overview||Episode overview||
||trakt_season||Episode season||
||trakt_episode||Episode Number||
||trakt_ep_id||Episode id string 'S01E01'||
||trakt_ep_abs_number||Episode absolute number||
||trakt_watched||`True` if watched on `username`'s profile||
||trakt_collected||`True` if collected on `username`'s profile||
----
'''Movie Metainfo'''

||movie_name||Movie name||
||movie_year||Production year||
||trakt_name||Trakt movie title||
||trakt_year||Trakt production year||
||trakt_movie_id||Movie Trakt.tv ID||
||trakt_movie_slug||Movie Trakt.tv slug||
||imdb_id||IMDB ID||
||tmdb_id||TMDB ID||
||trakt_tagline||Trakt tagline||
||trakt_overview||Trakt movie overview/description||
||trakt_released||Trakt release date||
||trakt_runtime||Movie runtime||
||trakt_rating||Movie Trakt.tv rating eg. 10/10||
||trakt_votes||Number of votes the rating is based on||
||trakt_language||Movie language||
||trakt_genres||Movie genres||
||trakt_movie_actors||Movie actors||
||trakt_watched||`True` if watched on `username`'s profile||
||trakt_collected||`True` if collected on `username`'s profile||
----
[[BR]]
'''trakt_watched and trakt_collected'''[[BR]]

If you specify an `account`/`username` in your config, two more fields are enabled `trakt_watched` and `trakt_collected`. These fields are set to `True` if the episode or movie entry has been marked as watched or collected respectively on the Trakt.tv account associated with `username`.

Example config to reject entries that have been marked as watched:

{{{
some_task:
  trakt_lookup:
    username: my_trakt_tv_username
  if:
   - trakt_watched: reject
}}}

'''Example'''[[BR]]

The most common uses we'll see are using it for [wiki:Plugins/make_rss make_rss] and making pretty filenames using [wiki:Plugins/set set] to set {{{content_filename}}} in the [wiki:Plugins/deluge deluge]. The 'default' jinja filter is used to insert 'Unknown' if trakt_lookup failes to get an entry field.
{{{
trakt_lookup: yes
set:
  content_filename: "{{series_name}} - {{series_id}} - {{trakt_ep_name|default('Unknown')}}"
}}}