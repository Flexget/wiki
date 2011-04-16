== Watched ==

This is generally not needed as series plugin will not download backwards from latest episode because of [wiki:Plugins/series/advancement episode advancement] functionality.

You can also use [wiki:Plugins/--inject inject] plugin to add some episode to history, thus preventing older ones being downloaded.

{{{
flexget --inject "Pioneer.One.S01E03.Imaginary" --feed <some series feed> --learn
}}}

This has the advantage of not cluttering your configuration file.

=== Example ===

{{{
series:
  - pioneer one:
      watched:
        season: 1
        episode: 3
}}}