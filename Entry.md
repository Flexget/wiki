---
title: Entry
description: 
published: true
date: 2022-12-07T06:02:48.321Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:49:18.595Z
---

# Entry
Entry represents a single item created by input(s), usually a downloadable content.
It contains all the information necessary for [plugins](/Plugins) to perform their job . Usually some [action](/FilterOperations) like accept or reject on the entry.

For example, the [regexp](/Plugins/regexp) plugin checks whether the given regular expression matches the entry's **title** or **url** and acts accordingly.

### Example of an entry

These are mandatory fields. You don't necessarily need to deal with anything more complicated for simple use cases.


| **Name** | **Value** |
| --- | --- |
| title | Linux Mint 17.3 cinnamon |
| url | http://torrents.linuxmint.com/torrents/linuxmint-17.3-cinnamon-64bit.iso.torrent |

### Known fields
Entry *may* have any of these fields, but is not *guaranteed* to have any of them. It may have other fields as well depending on configuration. 

>Use `--dump` option to see your task content as this list is not complete or always up-to-date.
{.is-warning}


| **Name** | **Created by** | **Description** |
| --- | --- | --- |
| id | multiple plugins | Set by metainfo plugins to the unique identifer for this entry. IE: "movie 2010" or "series S01E01" |
| path | multiple plugins | Path where this entry content should be saved |
| description | [rss](/Plugins/rss) | Item description |
| rss_pubdate | [rss](/Plugins/rss) | Date the RSS item was published |
| task | metainfo_task | Task name which this entry belongs to |
| quality | metainfo_quality, [series](/Plugins/series) | Detected quality, ie. `720p` |
| quality_req | [couchpotato](/Plugins/couchpotato) | A quality requirement string, can hold several qualities. Used by [movie_queue](/Plugins/movie_queue) |
| accessed | [filesystem](/Plugins/filesystem) | Last accessed time for the local file. Stored as a datetime object. |
| modified | [filesystem](/Plugins/filesystem) | Last modified time for the local file. Stored as a datetime object. |
| created | [filesystem](/Plugins/filesystem) | Creation time for the local file (only on Windows). Stored as a datetime object. |
| series_name | [series](/Plugins/series), metainfo_series | Series name |
| series_season | [series](/Plugins/series), metainfo_series | Series season |
| series_episode | [series](/Plugins/series), metainfo_series | Series episode |
| series_id | [series](/Plugins/series) | Series episode identifier, ie. `S01E02` or `2009-12-1` |
| series_date | [series](/Plugins/series) | The date of the episode. (only available for date based series) |
| proper | [series](/Plugins/series) | Whether this entry is a proper or repack release |
| argenteam_subtitle | [argenteam](/Searches/argenteam) | aRGENTeaM subtitle's url |
| imdb_url | [imdb_lookup](/Plugins/imdb_lookup)+others | Imdb url |
| imdb_id | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb identifier |
| imdb_name | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb name |
| imdb_original_name | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb original name |
| imdb_year | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb year |
| imdb_score | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb score |
| imdb_votes | [imdb_lookup](/Plugins/imdb_lookup)* | Imdb votes |
| imdb_genres | [imdb_lookup](/Plugins/imdb_lookup)* | List of imdb genres |
| imdb_languages | [imdb_lookup](/Plugins/imdb_lookup)* | List of imdb languages |
| imdb_photo | [imdb_lookup](/Plugins/imdb_lookup)* | Url for photo (hotlinking prevented) |
| imdb_plot_outline | [imdb_lookup](/Plugins/imdb_lookup)* | Plot outline |
| imdb_actors | [imdb_lookup](/Plugins/imdb_lookup)* | Actors dictionary (key: imdbid, value: name) |
| imdb_directors | [imdb_lookup](/Plugins/imdb_lookup)* | Directors dictionary (imdbid, name) |
| imdb_writers | [imdb_lookup](/Plugins/imdb_lookup)* | Writers dictionary (imdbid, name) |
| movie_name | [imdb_lookup](/Plugins/imdb_lookup)* | Movie title |
| movie_year | [imdb_lookup](/Plugins/imdb_lookup)* | Movie release year |
| output | [download](/Plugins/download) | Downloaded file |
| torrent | modify_torrent | When entry is a torrent this contains [Torrent class](/TorrentObject) |
| data | [download](/Plugins/download) | Internal. Binary content. |
| content_size | [content_size](/Plugins/content_size) | Parsed size of torrents or NZBs. |
| location | [filesystem](/Plugins/filesystem) | The local filename of the entry. |
| timestamp | [filesystem](/Plugins/filesystem) | The local file update time of the entry. |
| subtitles | [check_subtitles](/Plugins/check_subtitles) | A list of languages about subtitles founds on disk (local files only) |
| plex_server | [plex](/Plugins/plex) | If set, PMS hostname. Otherwise PMS IP. |
| plex_server_ip | [plex](/Plugins/plex) | PMS IP. |
| plex_port | [plex](/Plugins/plex) | PMS port. |
| plex_section | [plex](/Plugins/plex) | Section number. |
| plex_section_name | [plex](/Plugins/plex) | Section name. |
| plex_path | [plex](/Plugins/plex) | Entry path on PMS. |
| plex_duration | [plex](/Plugins/plex) | Entry length in seconds. |
| plex_thumb | [plex](/Plugins/plex) | Episode thumbnail, series only. |
| plex_art | [plex](/Plugins/plex) | Series or movie art as configured in PMS |
| plex_cover | [plex](/Plugins/plex) | Series cover for series, movie cover for movies. |
| plex_season_cover | [plex](/Plugins/plex) | Season cover, series only. If used in movies, movie cover will be set. |
| plex_title | [plex](/Plugins/plex) | Episode name as indexed on PMS. |
| plex_summary | [plex](/Plugins/plex) | Entry summary. |
| plex_status | [plex](/Plugins/plex) | Entry status: seen, inprogress or unwatched. |
| plex_url | [plex](/Plugins/plex) | Original plex url. |
| plex_userrating | [plex](/Plugins/plex) | Rating given by the user. From 1 to 10 |
| plex_key | [plex](/Plugins/plex) | Internal Plex identificator for the Media |
| tvdb_series_name | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series name provided by thetvdb |
| tvdb_rating | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series rating |
| tvdb_status | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series status(Continuing or Ended) |
| tvdb_runtime | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series runtime in minutes) |
| tvdb_first_air_date | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series premier date |
| tvdb_air_time | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series air time |
| tvdb_content_rating | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series content ration |
| tvdb_genres | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series genres |
| tvdb_network | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series network |
| tvdb_banner_url | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series banner url |
| tvdb_fanart_url | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series fanart url |
| tvdb_poster_url | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series poster url |
| tvdb_airs_day_of_week | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series airs date of the week |
| tvdb_actors | [thetvdb_lookup](/Plugins/thetvdb_lookup) | List of series actors |
| tvdb_language | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series language(en, fr, etc.) |
| imdb_url | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Series imdb url |
| zap2it_id | [thetvdb_lookup](/Plugins/thetvdb_lookup) |  |
| tvdb_ep_name | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode name |
| tvdb_ep_overview | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode plot |
| tvdb_ep_directors | [thetvdb_lookup](/Plugins/thetvdb_lookup) | List of episode directors |
| tvdb_ep_writers | [thetvdb_lookup](/Plugins/thetvdb_lookup) | List of episode writers |
| tvdb_ep_air_date | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode air date |
| tvdb_ep_rating | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode rating |
| tvdb_ep_guest_stars | [thetvdb_lookup](/Plugins/thetvdb_lookup) | List of episode guest stars |
| tvdb_ep_image_url | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode image url |
| tvdb_ep_id | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode season and number ie. S01E02 |
| tvdb_season | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode season |
| tvdb_episode | [thetvdb_lookup](/Plugins/thetvdb_lookup) | Episode number |
| trakt_series_name | [trakt_lookup](/Plugins/trakt_lookup) | Series name provided by trakt |
| trakt_series_runtime | [trakt_lookup](/Plugins/trakt_lookup) | Series runtime in minutes |
| trakt_series_first_aired_epoch | [trakt_lookup](/Plugins/trakt_lookup) | Series premier data in epoch time |
| trakt_series_first_aired_iso | [trakt_lookup](/Plugins/trakt_lookup) | Time stamp of premier date |
| trakt_series_air_time | [trakt_lookup](/Plugins/trakt_lookup) | Time the series ran |
| trakt_series_content_rating | [trakt_lookup](/Plugins/trakt_lookup) | Content rating ex: TV-14 |
| trakt_series_genres | [trakt_lookup](/Plugins/trakt_lookup) | Series genres |
| trakt_series_network | [trakt_lookup](/Plugins/trakt_lookup) | Series network |
| trakt_series_imdb_id | [trakt_lookup](/Plugins/trakt_lookup) | Series IMDB ID |
| trakt_series_tvdb_id | [trakt_lookup](/Plugins/trakt_lookup) | Series TVDB ID |
| trakt_series_tvrage_id | [trakt_lookup](/Plugins/trakt_lookup) | Series TVRage ID |
| trakt_series_actors | [trakt_lookup](/Plugins/trakt_lookup) | Series actors |
| trakt_series_country | [trakt_lookup](/Plugins/trakt_lookup) | Production Country |
| trakt_series_year | [trakt_lookup](/Plugins/trakt_lookup) | Series release year |
| trakt_series_status | [trakt_lookup](/Plugins/trakt_lookup) | Series status(ex: Airing) |
| trakt_series_overview | [trakt_lookup](/Plugins/trakt_lookup) | Series overview |
| trakt_ep_name | [trakt_lookup](/Plugins/trakt_lookup) | Episode name |
| trakt_ep_first_aired_epoch | [trakt_lookup](/Plugins/trakt_lookup) | Episode premier date in epoch |
| trakt_ep_first_aired_iso | [trakt_lookup](/Plugins/trakt_lookup) | Episode premier date time stamp |
| trakt_ep_overview | [trakt_lookup](/Plugins/trakt_lookup) | Episode overview |
| trakt_season | [trakt_lookup](/Plugins/trakt_lookup) | Episode season |
| trakt_episode | [trakt_lookup](/Plugins/trakt_lookup) | Episode Number |
| trakt_ep_id | [trakt_lookup](/Plugins/trakt_lookup) | Episode id string 'S01E01' |
| trakt_ep_tvdb_id | [trakt_lookup](/Plugins/trakt_lookup) | TVDB ID of episode |
| trakt_watched | [trakt_watched_lookup](/Plugins/trakt_watched_lookup) | Episode marked seen (true/false) |
| trakt_list | [trakt_emit](/Plugins/trakt_emit) | Names the originating list from which trakt_emit sourced this entry |
| tvmaze_series_weight | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series popularity |
| tvmaze_series_update_date | [tvmaze_lookup](/Plugins/tvmaze_lookup) | When series was last updated |
| tvmaze_series_webchannel | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series web channel (Netflix, Amazon, etc..) |
| tvmaze_series_show_type | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series type (scripted, reality, etc..) |
| tvmaze_series_episodes | [tvmaze_lookup](/Plugins/tvmaze_lookup) | List of episodes |
| tvmaze_series_id | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series ID provided by TVMaze |
| tvmaze_series_show_id | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series ID provided by TVMaze |
| tvmaze_series_name | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series name provided by TVMaze |
| tvmaze_series_year | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series year |
| tvmaze_series_rating | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series rating |
| tvmaze_series_status | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series status(Continuing or Ended) |
| tvmaze_series_summary | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series summary |
| tvmaze_series_runtime | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series runtime (in minutes) |
| tvmaze_series_premiered | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series premier date |
| tvmaze_genres | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series genres (list) |
| tvmaze_series_network | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series network |
| tvmaze_series_url | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series url |
| tvmaze_series_original_image | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series image url (large) |
| tvmaze_series_medium_image | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series image url (medium) |
| tvmaze_series_airdays | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series airs day of the week |
| tvmaze_series_language | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Series language(en, fr, etc.) |
| tvmaze_series_tvrage | [tvmaze_lookup](/Plugins/tvmaze_lookup) | tvrage ID as provided by TVMaze |
| tvmaze_episode_name | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode name |
| tvmaze_episode_airdate | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode air date |
| tvmaze_ep_runtime | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode runtime (in minutes) |
| tvmaze_episode_url | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode url |
| tvmaze_episode_original_image | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode image url (large) |
| tvmaze_episode_medium_image | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode image url (medium) |
| tvmaze_episode_season | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Season number of this episode. |
| tvmaze_episode_number | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode number. |
| tvmaze_episode_id | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Episode's TVMaze ID. |
| tvmaze_episode_airstamp | [tvmaze_lookup](/Plugins/tvmaze_lookup) | Date and Time Episode aired |
| tvmaze_series_actors | [tvmaze_lookup](/Plugins/tvmaze_lookup) | A list of the cast of the show. |

^* = and other plugins that utilize this plugin^