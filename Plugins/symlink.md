# Symlink

Unavailable on windows.

```text
symlink:
  to: <destination>
```

## Examples

Use your collection to create a symlinked imdb watchlist directory. Removals are not dealth with.

###

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
          login: '\{{ secrets.imdb.login }}'
          password: '\{{ secrets.imdb.pwd }}'
    fields:
      - imdb_id
    action: accept
  symlink:
    to: /storage/movies-watchlist/
```