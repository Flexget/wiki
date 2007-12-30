This module allows filtering based on IMDB score, votes and genres etc.

Results are cached so modifying configuration does not have an effect
on already filtered entries. This is done to reduce traffic to
IMDB now only once per movie. You can disable this TEMPORARILY by using
--no-cache argument. This will potentially affect other modules as well.

Configuration:

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

    # reject all entries which are not imdb-compatible
    # this has default value (True) even when key not present
    reject_invalid: True / False
}}}

== Entry fields (module developers): ==

    All fields are optional, but lack of required fields will
    result in filtering usually in default configuration (see reject_invalid).
{{{
    imdb_url       : Most important field, should point to imdb-movie-page (string)
    imdb_score     : Pre-parsed score/rating value (float)
    imdb_votes     : Pre-parsed number of votes (int)
    imdb_year      : Pre-parsed production year (int)
    imdb_genres    : Pre-parsed genrelist (array)
    imdb_languages : Pre-parsed languagelist (array)
}}}
    Supplying pre-parsed values may avoid checking and parsing from imdb_url.
    So supply them in your input-module if it's practical!