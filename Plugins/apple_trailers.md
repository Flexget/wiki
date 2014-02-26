= Input !AppleTrailers =

Adds support for [http://trailers.apple.com/ Apple Trailers] as an input source.

== Simple Configuration Example: ==

{{{
apple_trailers: 480p
accept_all: yes
download: ~/movies/trailers
}}}

This would download all trailers with 480p resolution. Resolution is a choice of 480p or 720p.

== Full Configuration Example: ==

{{{
apple_trailers:
  quality: 480p
  genres: ['Action and Adventure']
accept_all: yes
download: ~/movies/trailers
}}}

This would download all trailers in the Action and Adventure genre in 480p resolution. `quality` can be 480p or 720p. `genres` is a comma-separated list of genres to include from the list on [http://trailers.apple.com/#section=genres Apple's website]. If a trailer is not listed in a particular genre, it will not be downloaded.

== Entry Fields ==

This plugin populates the following entry fields:

`movie_name`: Name of the movie itself.

`movie_year`: Year movie is scheduled to be released, per Apple's website.

`movie_studio`: Studio releasing the movie, per Apple's website.

`apple_trailers_name`: The name of the clip itself, such as 'Trailer 1' or 'Winter Olympic Preview'.

`genres`: Comma separated list of genres, per Apple's website.

The above can be used if creating custom filenames with [wiki:Jinja Jinja].