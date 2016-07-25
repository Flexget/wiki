### List Match
This is a filter plugin that uses a list to accept or reject generated entries based on other list content. Any input can be used with [crossmatch](Plugins/crossmatch) plugin.

## Syntax
```yaml
list_match:
  from:
    - <list_type>: <list_name>
  action: [*accept*|reject]
  remove_on_match: [*yes*|no]
  single_match: [*yes*|no]
```

Default are marked with `*`.

By default, `list_match` will accept the first entry it sees from the list, so if there are multiple potential matches, only the first one will be used:
```yaml
discover:
  interval: 3 hour
    what:
      - movie_list: movies
    from:
      - kat:
          verified: yes
      - torrentz: verified
list_match:
  from:
    - movie_list: Looking
download: /downloads/
```

If you wish to match **ALL** entries and not just the first one, use the `single_match: no` option:

```yaml
rss: some_feed...
list_match:
  from:
    - trakt_list:
        username: traktusername
        list: watchlist
        type: movies
  single_match: no
download: /downloads/
```

All accepted entries are delete from list when task completes. To disable this, use the `remove_on_match: no` option:

```yaml
rss: some_feed...
list_match:
  from:
    - trakt_list:
        username: traktusername
        list: watchlist
        type: movies
  single_match: no
  remove_on_match: no
download: /downloads/
```

If you wish to reject entries based on a list, as opposed to accept, use `action: reject`:

```yaml
rss: some_feed...
list_match:
  from:
    - trakt_list:
        username: traktusername
        list: collection
        type: movies
  action: reject
download: /downloads/
```

## Use case examples:
This example shows you how to sync a list from Trakt in Flexget, if you remove an entry in Trakt, it will get removed from your my-watchlist in Flexget as well. (UNTESTED, need confirmation if this actually works)

```yaml
remove-from-list
  entry_list: my-watchlist
  list_match:
    from:
      - trakt_list:
          account: xxx
          list: watchlist
          type: shows
    action: reject # Will reject the entry if it's still in Trakt
    remove_on_match: no #Don't remove matched entries from Trakt, since that would clear all shows in Trakt, that are on your my-watchlist
  accept_all: yes
  list_remove:
    - entry_list: my-watchlist
```