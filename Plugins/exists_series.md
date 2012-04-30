= Existing series =

This plugin will reject all entries that represent an episode of a series that is already on disk.

=== Example ===

{{{
exists_series: /storage/series/
}}}

=== Example ===

{{{
exists_series: 
  - /storage/series/
  - /downloads/series/
}}}

== Advanced ==

By default, the exists_series will not allow downloading of different qualities of the same episode. (If you already have Lost.S01E01.hdtv, Lost.S01E01.720p will be rejected.) If you would like to allow different qualities of the same episode, you can use the advanced form of configuration, like so:

{{{
exists_series:
  path: /storage/series/
  allow_different_qualities: yes
}}}

If you would only like to allow qualities that are better than what is currently on disk, you can use this format:

{{{
exists_series:
  path: /storage/series/
  allow_different_qualities: better
}}}