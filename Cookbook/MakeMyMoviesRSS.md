== Recipe: My movie list ==

Generates RSS with imdb details, ordered by imdb score. Throw in [wiki:FilterImdbRated imdb_rated] and you get list of unwatched movies!

{{{
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
    directories: /storage/movies/
    make_rss:
      file: ~/public_html/movies.rss
      history: no
}}}

[wiki:TheCookBook Back to The Cook Book]