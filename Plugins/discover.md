# Discover
Creates entries based on search results. Queries are produced based on another input plugin(s).

<div class="alert alert-info" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  This may seem a bit scary at first, but just remember discover is normal input like rss!
</div>

Cookbook example: [discoverfeed](/Cookbook/Movies/discoverfeed)

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
  OR
  [release_estimations]:
    [optimistic]: <interval>
```

| Option | Default | Description |
| --- | --- | --- |
|limit| - | Set max results from each search engine. |
|interval| 5 hours| Time between trying searches again. |
|release_estimations|strict|Can be `loose`, `strict` or `ignore`, or `optimistic: <interval>`. <br/><br/> `strict` will reject all episodes/movies without air dates.<br/> `loose` will check for release dates, if release date can not be determined perform search anyway.<br/>`optimistic` sets the estimation mode to `strict` but starts searching `interval` units (eg. 7 days) before release date. <br/>`ignore` no release date checking will be attempted (try to use `optimistic` if possible).|

### Supported search engines
An overview of available search plugins can be found [here](/Searches). For a list of installed search plugins use command `flexget plugins --interface search`.

### Reruns
When using [next_series_episodes](/Plugins/next_series_episodes) as an input for `discover` it will attempt to retrieve new episodes until it fails to find more (up to 100 runs). The number of reruns can be limited with [max_reruns](/Plugins/max_reruns) plugin.

## Examples

### Search next series episodes
```yaml
discover:
  what:
    - next_series_episodes: yes
  from:
    - any supported search plugin
series:
  - name
```

Requires [series](/Plugins/series) configuration or [configure_series](/Plugins/configure_series) in the task.

### Search movie list
This example would produce results from the piratebay search engine based on the movies in the list "wanted_movies" in the [movie_list](/Plugins/List/movie_list) plugin. It will only search for movies that have a release date that is no more than 30 days in the future.

```yaml
tasks:
  discover-movies:
    discover:
      release_estimations:
        optimistic: 30 days
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
    - any supported search plugin
```

See [list_match](/Plugins/List/list_match) and [movie_list](/Plugins/List/movie_list) for further information.

