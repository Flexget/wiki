= Manage series easier with a preset =

With [wiki:ModulePreset preset] plugin you can avoid having to keep duplicate configuration in multiple feeds. This can be adapted for movies, comics etc. easily. See [wiki:ModulePreset preset] documentation for more tips.

{{{
series:
  download: ~/torrents/series/
  exists_series: ~/storage/series/
  series:
    - chuck
    - myth busters

feeds:
  some feed:
    rss: http://example.com/
    preset: series

  some another feed:
    rss: http://foobar.com/
    preset: series
}}}  

Uses plugins: [wiki:Plugin/preset preset], [wiki:Plugin/rss RSS], [wiki:Plugin/series series], [wiki:Plugins/exists_series exists_series],[wiki:Plugin/download download]

[wiki:TheCookBook Back to The Cook Book]