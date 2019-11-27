# Symlink
<div class="alert alert-warning" role="alert">
  <span class="glyphicon glyphicon-info-sign"></span>
  &nbsp;
  Unavailable on windows.
</div>

### Syntax:

|  Option  |  Values  |  Description  |
| --- | --- | --- |
| to | \<directory path> | Accepted entries are moved to this directory. Capable of *value replacement. Defaults to download path. Entry field `move_to` can be used to override the given path on a per entry basis. |
| existing | \<fail/ignore> | If the link already exists, choose to have the entry fail, or force the link to be replaced. Default is `fail`.
| rename | \<filename> | Accepted entries are renamed to this filename (inside of the `to` directory). Capable of *value replacement. |
| link_type | \<soft/hard> | Hardlinking directories creates new dirs and recursively hardlinks all files. Default is `soft`. |

*Note: Info on value replacement can be found in the example [here](https://flexget.com/Jinja). Commonly used replacement values come from the `Entry field` found [here](https://flexget.com/Entry)
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