== My movie list ==

Generates RSS with Imdb details, ordered by imdb score. Throw in [wiki:FilterImdbRated imdb_rated] and you get list of unwatched movies!

{{{
presets:
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
    preset: generate
    listdir: /storage/movies/
    make_rss:
      file: ~/public_html/movies.rss
      history: no
}}}

Uses plugins: [wiki:Plugins/preset preset], [wiki:Plugins/imdb_lookup imdb_lookup], [wiki:Plugins/make_rss make_rss], [wiki:Plugins/listdir listdir]