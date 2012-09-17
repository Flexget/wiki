= Manage series easier with a preset =

With [wiki:Plugins/preset preset] plugin you can avoid having to duplicate configuration in multiple feeds. This can be adapted for movies, comics etc. easily. See [wiki:Plugins/preset preset] documentation for more tips.

{{{
presets:
  tv:
    download: ~/torrents/series/
    exists_series: ~/storage/series/
    series:
      - pioneer one
      - south park

tasks:
  some feed:
    rss: http://example.com/
    preset: tv

  another feed:
    rss: http://foobar.com/
    preset: tv
}}}  

Uses plugins: [wiki:Plugins/preset preset], [wiki:Plugins/rss RSS], [wiki:Plugins/series series], [wiki:Plugins/exists_series exists_series], [wiki:Plugins/download download]

[wiki:Cookbook Back to The Cookbook]