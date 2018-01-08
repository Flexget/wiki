## Metainfo Movie
Allows parsing the received title by selected movie parser, and populating entry fields with relevant movie attributes.

### Syntax
```
metainfo_movie: yes
```

This will add the following fields to an entry:

- id (eg: `Cool Movie 2010`)
- `movie_parser`
- `movie_name`
- `movie_year`
- `proper`
- `proper_count`

If selected movie [parser](/Plugins/parsing) is guessit, the following fields will also be added:

- `is_3d`
- `subtitle_languages`
- `languages`
- `video_codec`
- `video_profile`
- `format`
- `audio_codec`
- `audio_channels`
- `audio_profile`
- `screen_size`
- `release_group`