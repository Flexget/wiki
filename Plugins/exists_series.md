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

By default, the exists_series will not allow downloading of multiple qualities of the same episode. If you would like to allow that, you can use the advanced form of configuration, like so:

{{{
exists_series:
  path: /storage/series/
  allow_qualities: yes
}}}