= Existing movies =

This plugin will reject all entries that represent an movie that is already on disk. This works only for imdb compatible entries.

=== Example ===

{{{
exists_movie: /storage/movies/
}}}

=== Example ===

{{{
exists_movie: 
  - /storage/movies-sd/
  - /storage/movies-hd/
}}}
