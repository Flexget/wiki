= Downloading Apple Trailers =

=== Quick Start ===

 [wiki:Plugins/apple_trailers Apple Trailers Plugin]::

=== Downloading Trailers By Genre ===

This method involves looking up movie titles through the [wiki:Plugins/imdb imdb] plugin. It then filters out the genres you don't want included. In the example below, the genres of Documentary, Foreign, Comedy, Fantasy, or Musical were rejected.

{{{
AppleTrailers:
  apple_trailers: 720p
  imdb:
    reject_genres:
      - documentary
      - foreign
      - comedy
      - fantasy
      - musical
  download: J:\FTP\Trailers
  set:
    filename: '{{title}} - Trailer - 720p.mov'
}}}


[wiki:Cookbook Back to The Cookbook]