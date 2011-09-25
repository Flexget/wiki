== Watched ==

This is generally not needed as series plugin will not download backwards from latest episode because of [wiki:Plugins/series/advancement episode advancement] functionality.

Alternatively you can use [wiki:Plugins/--inject inject] plugin to add some episode into history, thus preventing older ones being downloaded. If you have specified quality requirements for the series, make sure to include the appropriate quality in the episode name.

{{{
flexget --inject "Pioneer.One.S01E03.Imaginary.720p" --feed <some series feed> --learn
}}}

This has the advantage of not cluttering your configuration file.

=== Example ===

{{{
series:
  - pioneer one:
      watched: S01E03
}}}

=== Old format ===

{{{
series:
  - pioneer one:
      watched: 
        season: 1
        episode: 3
}}}