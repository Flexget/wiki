= Downloading Apple Trailers =

=== Quick Start ===

 [wiki:Plugins/apple_trailers Apple Trailers Plugin]::

=== Downloading Trailers By Genre ===

This method involves looking up movie titles through the [wiki:Plugins/imdb_lookup imdb_lookup] plugin or the [wiki:Plugins/thetvdb_lookup thetvdb_lookup] plugin. It is then followed up with an [wiki:Plugins/if if] filter to sort out the genres you don't want included. In the example below, the genres of Documentary, Foreign, Comedy, Fantasy, or Musical were rejected.

{{{
AppleTrailers:
  rss: http://trailers.apple.com/trailers/home/rss/newtrailers.rss
  imdb_lookup: yes
  if:
    - "any(genre in ['documentary', 'foreign', 'comedy', 'fantasy', 'musical'] for genre in imdb_genres)": reject
  set:
    filename: '{{title}} - Trailer - 720p.mov'
}}}

[wiki:Cookbook Back to The Cookbook]