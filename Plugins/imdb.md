= Filter IMDB =

This module allows filtering based on IMDB score, votes and genres etc.
Results are cached so this doesn't cause unnecessary load to [http://www.imdb.com imdb].

'''Note:''' If [wiki:Entry] doesn't have `imdb url` present plugin will try to use imdb's search function. This does not work on 100% of cases and in some rare cases it may even get wrong movie details.

=== Example ===

{{{
imdb:
  min_score: 6.2
  min_votes: 5000
  reject_genres:
    - horror
}}}

=== Full configuration ===

{{{
Note: All parameters are optional. Some are mutually exclusive.

min_score: <num>
min_votes: <num>
min_year: <num>

# reject if genre contains any of these
reject_genres:
  - genre1
  - genre2

# reject if language contain any of these
reject_languages:
  - language1

# accept only this language
accept_languages:
  - language1

# NOTE: all persons are identified by their IMDb ID
# You can use names as well but they need to be exact matches.

# accept movies with any of these actors
accept_actors:
    - nm0004695
    - nm0004754

# reject movie if it has any of these actors
reject_actors:
    - nm0001191
    - nm0002071

# accept all movies by these directors
accept_directors:
    - nm0000318

# reject movies by these directors
reject_directors:
    - nm0093051
}}}

'''Note:''' To reject non imdb compatible entries, use [wiki:Plugins/imdb_required imdb_required] plugin.