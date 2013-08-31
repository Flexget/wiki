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


''Note: As of version 1.1.98 plugin will follow symbolically linked directories.
''