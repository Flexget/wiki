---
title: trakt_lookup
description: 
published: true
date: 2022-09-18T05:28:30.871Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:15:09.550Z
---

# Trakt Lookup

This plugin returns series information from Trakt.tv. The name of the series usually has to be VERY close to what's shown on Trakt.  
If you are having problems returning the correct information for a show, please add the `tvdb_id` to the series using the [set](/Plugins/series/set) plugin.  

<div class="alert alert-info" role="alert">

Please see [Trakt Authentication](/Trakt_Authentication) for how to authorize Flexget to access your private Trakt.tv account.</div>


#### Syntax

```yaml
trakt_lookup: yes
```
or

```YAML
trakt_lookup:
   account: <flexget account name>
   username: <trakt username>
```

**NOTE**: `username` is the user for which you wish to lookup specific information such as collection, watched history or user ratings. The `account` option is required if your profile is private, and is the account name that was set during [Trakt authentication](/Trakt_Authentication).

**Series Metainfo**

| Trakt_lookup Field | Description |
| --- | --- |
| trakt_series_name | Series name provided by trakt  |
| trakt_series_year | Series release year  |
| imdb_id | Series IMDB ID  |
| tvdb_id | Series TVDB ID  |
| tmdb_id | Series TMDB ID  |
| trakt_id | Series Trakt.tv ID  |
| tvrage_id | Series TVRage ID  |
| trakt_slug | Series Trakt.tv slug eg. `the-matrix`  |
| trakt_series_runtime | Series runtime in minutes  |
| trakt_series_air_time | Time the series ran/runs ex: `'21:00'`  |
| trakt_series_air_day | Day the series ran/runs ex: `'Thursday'`  |
| trakt_series_content_rating | Content rating ex: `TV-14`  |
| trakt_genres | List of series genres ex: `'comedy, drama'`  |
| trakt_series_network | Series network  |
| imdb_url | IMDB url for linking  |
| trakt_series_url | Trakt url for linking  |
| trakt_series_country | Series country origin  |
| trakt_series_status | Series status ie. `returning series` (airing right now), `in production` (airing soon), `planned` (in development), `canceled` or `ended`  |
| trakt_series_overview | Series overview/description  |
| trakt_series_rating | Series rating on Trakt.tv eg. 8/10  |
| trakt_series_votes | Series votes  |
| trakt_series_aired_episodes | Number of aired episodes  |
| trakt_series_episodes | List of episode titles  |
| trakt_actors | Series actors  |

`New To Series`

| Trakt_lookup fields  |  Description  |
| --- | --- |
| trakt_languages |  List of available translations in iso-36 |
| trakt_translations |  List of dictionaries all translations from languages |
| trakt_homepage |  Network's page for linking |
| trakt_trailer |  Trailer if available |
----

#### Episode Metainfo

| Trakt_lookup Field  |  Description  |
| --- | --- |
| trakt_ep_name |  Episode name  |
| trakt_ep_tvdb_id |  TVDB ID of episode  |
| trakt_ep_imdb_id |  IMDb ID of episode  |
| trakt_ep_tmdb_id |  TMDB ID of episode  |
| trakt_ep_tvrage_id |  TVRage ID of episode  |
| trakt_ep_first_aired |  Episode premier date  |
| trakt_ep_overview |  Episode overview  |
| trakt_season |  Episode season  |
| trakt_episode |  Episode Number  |
| trakt_ep_id |  Episode id string 'S01E01'  |
| trakt_ep_abs_number |  Episode absolute number  |
| trakt_watched |  `True` if watched on `username`'s profile  |
| trakt_collected |  `True` if collected on `username`'s profile  |

----
**Movie Metainfo**

| Trakt_lookup Field  |  Description  |
| --- | --- |
| movie_name |  Movie name  |
| movie_year |  Production year  |
| trakt_movie_name |  Trakt movie title  |
| trakt_movie_year |  Trakt production year  |
| trakt_movie_id |  Movie Trakt.tv ID  |
| trakt_slug |  Movie Trakt.tv slug  |
| imdb_id |  IMDB ID  |
| tmdb_id |  TMDB ID  |
| trakt_tagline |  Trakt tagline  |
| trakt_overview |  Trakt movie overview/description  |
| trakt_released |  Trakt release date  |
| trakt_runtime |  Movie runtime  |
| trakt_rating |  Movie Trakt.tv rating eg. 10/10  |
| trakt_votes |  Number of votes the rating is based on  |
| trakt_language |  Movie language  |
| trakt_genres |  Movie genres  |
| trakt_actors |  Movie actors  |
| trakt_watched |  `True` if watched on `username`'s profile  |
| trakt_collected |  `True` if collected on `username`'s profile  |

`New to Movies`

| Trakt_lookup Field  |  Description  |
| --- | --- |
| trakt_homepage |  Network's page for linking  |
| trakt_trailer |  Trailer if available  |
| trakt_languages |  List of available translations  |
| trakt_translations |  List of dictionaries all translations from languages  |
----

| Trakt_lookup Actors fields  |  Description  |
| --- | --- |
| trakt_actors.id  |  actor trakt id  |
| trakt_actors.name |  actor name  |
| trakt_actors.slug |  trakt slug for actor  |
| trakt_actors.tmdb |  TMDB id for actor  |
| trakt_actors.imdb |  IMDB id for actors  |
| trakt_actors.biograph |  Wikipedia overview for actor  |
| trakt_actors.birthday |  Birthday of actors in python.date format  |
| trakt_actors.death |  Date actor died in python.date format  |
| trakt_actors.homepage |  Official url for actor  |


`NOT ALL FIELS AVAILABLE`

| Trakt_lookup translations fields  |  Description  |
| --- | --- |
| trakt_translations.language |  alpha2 code for language  |
| trakt_translations.overview |  Translated overview  |
| trakt_translations.tagline |  Translated tagline  |
| trakt_translations.title |  Translated title  |

#### Notes:

* [Trakt on Images](http://docs.trakt.apiary.io/#introduction/images)
* [More information](http://docs.trakt.apiary.io/#introduction/standard-media-objects)

## Examples

#### Set filename

The most common uses we'll see are using it for [make_rss](/Plugins/make_rss) and making pretty filenames using [set](/Plugins/set) to set `content_filename` in the [deluge](/Plugins/deluge). The 'default' jinja filter is used to insert 'Unknown' if trakt_lookup failes to get an entry field.

```
trakt_lookup: yes
set:
  content_filename: "{{series_name}} - {{series_id}} - {{trakt_ep_name|default('Unknown')}}"
```

#### Reject entries that have been marked as watched

```
some_task:
  trakt_lookup:
    username: my_trakt_tv_username
  if:
    - trakt_watched: reject
```
