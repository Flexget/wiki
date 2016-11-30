### List Match

<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

This is a filter plugin that uses a list to accept or reject generated entries based on other list content. For operating any input  see [crossmatch](/Plugins/crossmatch) plugin instead.

## Syntax

```text
list_match:
  from:
    - <list_type>: <list_name>
  action: [accept|reject]
  remove_on_match: [yes|no]
  single_match: [yes|no]
```

|Option|Default|
|---|---|
|action|accept|
|remove_on_match|yes|
|single_match|yes|

By default, `list_match` will accept the first entry it sees from the list, so if there are multiple potential matches, only the first one will be used.

If you wish to match **all** entries and not just the first one, use the `single_match: no` option.

All accepted entries are deleted from list when task completes. To disable this, use the `remove_on_match: no` option.

If you wish to reject entries based on a list, as opposed to accept, use `action: reject`.

### Examples

#### Download queued movies


```yaml
rss: http://example.com/rss
proper_movies: yes
seen_movies: loose
list_match:
  from:
    - movie_list: movies
quality: 720p+ bluray
```

This requires that [movie list](/Plugins/List/movie_list) is either managed by hand or synced automatically from other sources. Check [movie list](/Plugins/List/movie_list) page for more information about that.

#### Sync lists (untested)
This example shows you how to sync a list from Trakt in Flexget, if you remove an entry in Trakt, it will get removed from your my-watchlist in Flexget as well. 

```yaml
remove-from-list
  entry_list: my-watchlist
  list_match:
    from:
      - trakt_list:
          account: xxx
          list: watchlist
          type: shows
    action: reject 
    remove_on_match: no
  accept_all: yes
  list_remove:
    - entry_list: my-watchlist
```
Notes:
* `action: reject` -- will reject the entry if it's still in Trakt.
* `remove_on_match: no` -- Don't remove matched entries from Trakt, since that would clear all shows in Trakt, that are on your my-watchlist
