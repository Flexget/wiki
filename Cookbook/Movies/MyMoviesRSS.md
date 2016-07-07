## My movie list
Generates RSS with Imdb details, ordered by imdb score. Throw in [imdb_rated](/Plugins/imdb_rated) and you get list of unwatched movies!

```
templates:
  generate:
    interval: 4 hours
    accept_all: yes
    imdb_lookup: yes
    disable_builtins: yes
    sort_by:
      field: imdb_score
      reverse: yes

feeds:

  storage_movies:
    template: generate
    filesystem: /storage/movies/
    make_rss:
      file: ~/public_html/movies.rss
      history: no
```

Uses plugins: [template](/Plugins/template), [imdb_lookup](/Plugins/imdb_lookup), [make_rss](/Plugins/make_rss), [filesystem](/Plugins/filesystem)