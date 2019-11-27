# Symlink
<div class="alert alert-warning" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  Unavailable on windows.
</div>

# Move

### Syntax:

|Option|Description|
|---|---|
|to| Directory to move accepted entries to, allows value replacement, defaults to download path. Entry field `move_to` can be used to override given path per entry basis.|
|existing| *fail* (default), *ignore* |
|rename| The actual filename inside the 'to' directory to rename the entries, allows value replacement. |
|link_type| *soft* (default), *hard*. Supports hardlinking directories (creates new dirs and recursively hardlinks all files). |

## Examples


### Watchlist directory

Use your collection to create a symlinked imdb watchlist directory. Removals are not dealt with.

```yaml
link-watchlist-movies:
  interval: 4 hours
  history: no
  seen: local
  filesystem:
    - /storage/movies/
  imdb_lookup: yes
  crossmatch:
    from:
      - imdb_list:
          list: watchlist
          login: '{? imdb.login ?}'
          password: '{? imdb.pwd ?}'
    fields:
      - imdb_id
    action: accept
  symlink:
    to: /storage/movies-watchlist/
```