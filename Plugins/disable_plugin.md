= Disable plugin =

Allows disabling plugins when using [wiki:Plugin/preset presets].

=== Example ===

{{{
movies:
  download: ~/torrents/movies/
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

Feed nzbs uses all other configuration from preset movies but removes the download plugin and instead uses [wiki:Plugin/sabnzbd sabnzbd].