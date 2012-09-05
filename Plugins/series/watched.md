== Watched ==

This is generally not needed as series plugin will not download backwards from latest episode because of [wiki:Plugins/series/advancement episode advancement] functionality.

Alternatively you can use [wiki:Plugins/--inject inject] plugin to add some episode into history, thus preventing older ones being downloaded. If you have specified quality requirements for the series, make sure to include the appropriate quality in the episode name.

{{{
flexget --inject "Pioneer.One.S01E03.Imaginary.720p" --task <some series task> --learn
}}}

This has the advantage of not cluttering your configuration file and it works with [wiki:Plugins/all_series all_series] and other solutions that do not list series in the configuration file.
'''Note:''' If you already have other episodes in the series history, you may also need to add the {{{--disable-advancement}}} flag to this command.

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