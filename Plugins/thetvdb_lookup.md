# TheTVDB Lookup
For most purposes, the series name is sufficient to get a match on TheTVDB. If you can't get a match (e.g., multiple IDs defined for a series name) then you can provide the tvdb_id from their website to bypass the matching process.

```yaml
series:
  - some_series:
      set:
        tvdb_id: <tvdb_id>
```

This plugin looks up more information from thetvdb.com about any entries that FlexGet has identified as series. thetvdb_lookup will populate several more entry fields that can be used in other plugins.


| tvdb_series_name | Series name provided by thetvdb |
| --- | --- |
| tvdb_url | Series thetvdb URL |
| tvdb_rating | Series rating |
| tvdb_status | Series status(Continuing or Ended) |
| tvdb_runtime | Series runtime (in minutes) |
| tvdb_first_air_date | Series premier date |
| tvdb_air_time | Series air time |
| tvdb_content_rating | Series content ration |
| tvdb_genres | Series genres |
| tvdb_network | Series network |
| tvdb_banner_url | Series banner url |
| tvdb_fanart_url | Series fanart url |
| tvdb_poster_url | Series poster url |
| tvdb_airs_day_of_week | Series airs date of the week |
| tvdb_actors | Series actors |
| tvdb_language | Series language(en, fr, etc.) |
| imdb_url | Series imdb url |
| imdb_id |  |
| zap2it_id |  |
| tvdb_id |  |
| tvdb_ep_name | Episode name |
| tvdb_ep_overview | Episode plot |
| tvdb_ep_directors | Episode directors |
| tvdb_ep_writers | Episode writers |
| tvdb_ep_air_date | Episode air date |
| tvdb_ep_rating | Episode rating |
| tvdb_ep_guest_stars | Episode guest stars |
| tvdb_ep_image_url | Episode image url |
| tvdb_season | Season number of this episode. |
| tvdb_episode | Episode number. |
| tvdb_ep_id | Season and episode in SxxEyy format. |
| tvdb_absolute_number | Absolute number of this episode. |

**Example:**

The most common use is to look up an episode title that can be used to format a pretty filename. This example uses `tvdb_ep_name` as parsed by thetvdb_lookup in the [set](/Plugins/set) plugin to set `content_filename` (which the [deluge](/Plugins/deluge) plugin uses to rename the main file within a torrent.) The 'default' jinja filter is used to insert 'Unknown' if thetvdb_lookup fails to get an tvdb_ep_name for the entry.
```
thetvdb_lookup: yes
set:
  content_filename: "{{ series_name }} - {{ series_id }} - {{ tvdb_ep_name|default('Unknown') }}  - {{ quality|upper }}"
```