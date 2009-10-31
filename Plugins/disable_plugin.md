= Disable plugin =

Allows disabling plugins when using [wiki:Plugins/preset presets].

=== Example ===

{{{
movies:
  download: ~/torrents/movies/
  imdb:
    min_score: 6.2
    .
    .

feeds:
  nzbs:
    preset: movies
    disable_plugin:
      - download
    sabnzbd:
      .
      .
}}}

Feed nzbs uses all other configuration from preset movies but removes the download plugin and instead uses [wiki:Plugins/sabnzbd sabnzbd].