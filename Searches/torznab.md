# torznab
Designed to search using Torznab indexers with with [discover](/Plugins/discover) plugins. Tested using [Jackett](https://github.com/Jackett/Jackett), though should work with any Torznab indexer.

## Config format
```text
discover:
  what:
    - ...
  from:
    - torznab:
        website: <torznab feed url>
        apikey: <apikey>
        [searcher]: <value>
        [categories]: <values>
```
| Option | Default | Description |
| --- | --- | --- |
|searcher| search | Can be `movie`, `tv`, `tvsearch` or `search`. <br/><br/>`tv` and `tvsearch` are aliases.<br/>`tv` and `movie` both take advantage of metadata provided by torznab feeds and matches the results with metadata available in the flexget entry already (trakt_id, imdb_id, etc.).<br/>`search` is a simple search without the additional checks described above. |
|categories| -| List of znab categories to restrict the search to, see [newznab documentation](https://newznab.readthedocs.io/en/latest/misc/api/#predefined-categories) for the category ids. |

## Examples
### Search for movies from trakt watchlist
```yaml
tasks:
  discovermovies:
    discover:
      what:
        - trakt_list:
            username: <trakt username>
            account: <account set up in CLI>
            list: watchlist
            type: movies
      from:
        - torznab:
            website: http://jackett:9117/api/v2.0/indexers/all/results/torznab/
            apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
            searcher: movie
    accept_all: yes
    trakt_lookup: yes
    quality: 1080p+
    duplicates:
      field: imdb_id
      action: reject
    sort_by:
      - quality
      - torrent_availability
      - torrent_seeds
    transmission:
      username: transmission
      add_paused: Yes
```
### Search for HD tv shows
```yaml
torznab:
  website: http://jackett:9117/api/v2.0/indexers/all/results/torznab/api
  apikey: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
  searcher: tv
  categories:
    - 5040
```