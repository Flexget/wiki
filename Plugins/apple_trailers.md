= Input !AppleTrailers =

Adds support for [http://trailers.apple.com/ Apple Trailers] as an input source.

== Example: ==

{{{
apple_trailers: 480p
accept_all: yes
download: ~/movies/trailers
}}}

This would download all trailers with 480p resolution. Resolution is a choice of 480p or 720p.

This plugin populates two extra entry fields, `movie_name` and `apple_trailers_name`. `movie_name` is self explanatory, and `apple_trailers_name` contains the name of the particular clip, for example 'Clip 2' or 'Trailer'. These can be used if creating custom filenames with [wiki:Jinja Jinja].