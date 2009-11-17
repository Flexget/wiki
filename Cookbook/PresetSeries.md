= Manage series easier with a preset =

With [wiki:ModulePreset preset] plugin you can avoid having to keep duplicate configuration in multiple feeds. This can be adapted for movies, comics etc. easily. See [wiki:ModulePreset preset] documentation for more tips.

{{{
tv:
  download: ~/torrents/series/
  exists_series: ~/storage/series/
  series:
    - chuck
    - myth busters

feeds:
  some feed:
    rss: http://example.com/
    preset: tv

  some another feed:
    rss: http://foobar.com/
    preset: tv
}}}  

Uses plugins: [wiki:Plugins/preset preset], [wiki:Plugins/rss RSS], [wiki:Plugins/series series], [wiki:Plugins/exists_series exists_series],[wiki:Plugins/download download]

[wiki:Cookbook Back to The Cookbook]