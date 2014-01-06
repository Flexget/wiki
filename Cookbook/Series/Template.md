= Manage series easier with a preset =

With [wiki:Plugins/preset preset] plugin you can avoid having to duplicate configuration in multiple tasks. This can be adapted for movies, comics etc. easily. See [wiki:Plugins/preset preset] documentation for more tips.

{{{
templates:
  tv:
    download: ~/torrents/series/
    exists_series: ~/storage/series/
    series:
      - pioneer one
      - south park

tasks:
  some feed:
    rss: http://example.com/
    template: tv

  another feed:
    rss: http://foobar.com/
    template: tv
}}}  

Uses plugins: [wiki:Plugins/template template], [wiki:Plugins/rss RSS], [wiki:Plugins/series series], [wiki:Plugins/exists_series exists_series], [wiki:Plugins/download download]

[wiki:Cookbook Back to The Cookbook]