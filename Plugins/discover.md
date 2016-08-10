# Discover
Creates entries based on search results. Queries are produced based on another input plugin(s).

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  This may seem a bit scary, but just remember discover is normal input like rss!
</div>

## Config Format
```text
discover:
  what:
    - <input plugin config>
  from:
    - <search plugin>
  [limit]: <value>
  [interval]: <value>
  [release_estimations]: <value>
```

| Option | Description |
| --- | --- |
|limit| max results from each search engine|
|interval|time between trying each search again. Default is 5 hours|
|release_estimations|Can be `auto`, `strict` or `ignore`. If set to `ignore`, no release date checking will be attempted. If set to `strict`, will reject all episodes without air dates. Default is `auto`, which will check all episodes for air dates, but won't reject those with missing air dates.|

### Supported search engines
An overview of available search plugins can be found [here](/Searches). For a list of installed search plugins run `flexget plugins --group search`.

### Examples


#### Search next series episodes
```yaml
discover:
  what:
    - next_series_episodes: yes
  from:
    - value
```

It's also possible to have inputs directly looked up here (but not advised as it would look up each time and not appear in your queues):

```yaml
discover:
  what:
    - imdb_list:
        list: watchlist
    - trakt_list:
        account: USERNAME
        list: watchlist
        type: movies
    - movie_list: listname
  from:
    - value
```

#### Search movie list
This example would produce results from the piratebay search engine based on the movies in the list "wanted_movies" in the [movie_list](/Plugins/List/movie_list) plugin.

```yaml
tasks:
  discover-movies:
    discover:
      what:
        - movie_list: wanted_movies
      from:
        - piratebay:
            category: "highres movies"
            sort_by: seeds
      interval: 1 day
    list_match:
      from:
        - movie_list: wanted_movies
```

See [list_match](/Plugins/List/list_match) and [movie_list](/Plugins/List/movie_list) for further information.