= Existing movies =

This plugin will reject all entries that represent an movie that is already on disk.

== Syntax ==

{{{
exists_movie:
  path: /path/to/movies
  [type]: {dirs|files}
  [allow_different_qualities]: {better|yes|no}
  [lookup]: {imdb|no}
}}}


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

== Advanced ==
=== type ===
By default, exists_movie will scan for directories within the given folder(s). If you would like to scan for files instead, use:

{{{
exists_movie:
  path: /storage/movies
  type: files
}}}

=== allow_different_qualities ===
By default, the exists_movie will not allow downloading of different qualities of the same movie. (If you already have Moon.720p, Moon.1080p will be rejected.) If you would like to allow different qualities of the same movie, you can use the advanced form of configuration, like so:

{{{
exists_movie:
  path: /storage/movies
  allow_different_qualities: yes
}}}

If you would only like to allow qualities that are better than what is currently on disk, you can use this format:

{{{
exists_movie:
  path: /storage/movies
  allow_different_qualities: better
}}}

=== lookup ===
By default, exists_movie will use the internal movie parser. If you would like to use imdb_lookup instead, use:

{{{
exists_movie:
  path: /storage/movies
  lookup: imdb
}}}


''Note: As of version 1.1.98 plugin will follow symbolically linked directories.
''