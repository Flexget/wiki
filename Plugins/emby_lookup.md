# Emby lookup
Performs [Emby](https://emby.media/) search for all entries in the feed  .

```yaml
emby_lookup:
  host: http://emby.localhost:8096
  username: flexget
  password: flexget
  return_host: wan
```
emby_lookup will populate several entry fields that can be used in other plugins.


## Genaral Fields
| Name | Description |
| --- | --- |
| emby_id | The Emby ID |
| emby_name | Name of media |
| emby_fullname | Complete name of media |
| emby_type | Type of media |
| emby_created_date | Date media was created in Emby |
| emby_path | Path in emby |
| emby_filename | File name |
| emby_file_extension | File extension |
| emby_watched | Watched status |
| emby_favorite | Is favorite |
| emby_playcount | Play Count |
| emby_format_3d | 3D format |
| emby_quality | Quality for emby |
| emby_subtitles | Loaded subtitles in emby | 
| emby_download_url | Url for media downlod |
| emby_library_name| Library name in emby |
| emby_page| Emby Page |

## Series Fields
| Name | Description |
| --- | --- |
| emby_serie_year | Series year |
| emby_serie_aired_date | Series aired date|
| emby_serie_id | Series ID |
| emby_serie_name | Series name | 
| emby_serie_photo | Series photo | 
| emby_serie_imdb_id | Series imdb id |
| emby_serie_tvdb_id | Series tvdb id |
| emby_serie_overview | Series overview |
| emby_serie_page | Series page | 

## Season Fields
| Name | Description |
| --- | --- |
| emby_season | Series season |
| emby_season_name | Series season name|
| emby_season_id | Series season ID |
| emby_season_page | Series season page | 
| emby_season_photo | Series season photo | 
| emby_season_imdb_id | Series season imdb id |
| emby_season_tmdb_id | Series season tmdb id |
| emby_season_tvdb_id | Series season tvdb id |

## Episode Fields
| Name | Description |
| --- | --- |
| emby_episode | Series episode |
| emby_ep_name | Series episode name|
| emby_ep_id | Series episode ID |
| emby_ep_page | Series episode page | 
| emby_ep_photo | Series episode photo | 
| emby_ep_imdb_id | Series episode imdb id |
| emby_ep_tmdb_id | Series episode tmdb id |
| emby_ep_tvdb_id | Series episode tvdb id |
| emby_ep_aired_date | Series episode aired date |
| emby_ep_overview | Series episode overview |

## Movie Fields
| Name | Description |
| --- | --- |
| emby_movie_name | Movie Name |
| emby_movie_year | Movie year |
| emby_movie_id | Movie ID |
| emby_movie_page | Movie page | 
| emby_movie_photo | Movie   photo | 
| emby_movie_imdb_id | Movie imdb id |
| emby_movie_tmdb_id | Movie tmdb id |
| emby_movie_aired_date | Movie aired date |
| emby_movie_overview | Movie overview |

#### Example

The most common use is to look up a movie title that can be used to format a pretty filename. This example uses `emby_movie_name` and `emby_movie_year` as parsed by emby_lookup in the [set](/Plugins/set) plugin to set `content_filename` (which the [deluge](/Plugins/deluge) plugin uses to rename the main file within a torrent).

```yaml
emby_lookup:
  host: http://emby.localhost:8096
  username: flexget
  password: flexget
  
set:
  content_filename: '{{ emby_movie_name }} ({{ emby_movie_year }})'
```