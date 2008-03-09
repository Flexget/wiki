= Filter IMDB =

This module allows filtering based on IMDB score, votes and genres etc.
Results are cached so this doesn't cause unnecessary load to [http://www.imdb.com imdb].

'''Important note:''' If [wiki:Entry] does not have direct imdb url present !FilterImdb will try to use imdb's search function. This does not work on 100% of cases, and in some rare cases it may even get wrong movie details. This module works best when input module provides accurate urls for entries, currently only [wiki:InputRlsLog RlsLog] does that.

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
filter_invalid: True / False
}}}