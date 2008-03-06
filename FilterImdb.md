= Filter IMDB =

This module allows filtering based on IMDB score, votes and genres etc.
Results are cached so doesn't cause unnecessary load to [http://www.imdb.com imdb].

Note: [wiki:Entry] must have imdb url present in order to [wiki:FilterImdb] to function properly. Currently only [wiki:InputRlsLog RlsLog] module provides this. In future [wiki:FilterImdb] will be able to use imdb search function to try to overcome missing imdb urls since they're rarely available.

=== Configuration: ===

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

# reject all [wiki:entry entries] which are not imdb-compatible
# this has default value (True) even when key not present
reject_invalid: True / False
}}}