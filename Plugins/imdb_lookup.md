# IMDB lookup
Performs [IMDB](http://www.imdb.com) search for all entries in the feed and provides IMDB lookup functionality to other plugins.

```
imdb_lookup: yes
```
imdb_lookup will populate several entry fields that can be used in other plugins.

| Name | Description |
| --- | --- |
| imdb_url | Imdb url |
| imdb_id | Imdb identifier |
| imdb_name | Imdb name |
| imdb_original_name | Imdb original name |
| imdb_year | Imdb year |
| imdb_score | Imdb score |
| imdb_votes | Imdb votes |
| imdb_genres | List of imdb genres |
| imdb_languages | List of imdb languages |
| imdb_photo | Url for photo (hotlinking prevented) |
| imdb_plot_outline | Plot outline |
| imdb_actors | Actors dictionary (key: imdbid, value: name) |
| imdb_directors | Directors dictionary (imdbid, name) |
| imdb_writers | Writers dictionary (imdbid, name) | 
| imdb_mpaa_rating | MPAA Rating

#### Example

The most common use is to look up a movie title that can be used to format a pretty filename. This example uses `imdb_name` and `imdb_year` as parsed by imdb_lookup in the [set](/Plugins/set) plugin to set `content_filename` (which the [deluge](/Plugins/deluge) plugin uses to rename the main file within a torrent).
```
imdb_lookup: yes
set:
  content_filename: "{{ imdb_name }} ({{ imdb_year }}) - {{ quality|upper }}"
```