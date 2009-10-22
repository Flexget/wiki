= Manage series easier with a preset =

With [wiki:ModulePreset preset] plugin you can avoid having to keep duplicate configuration in multiple feeds. This can be adapted for movies, comics etc. easily. See [wiki:ModulePreset preset] documentation for more tips.

{{{
series:
  download: ~/torrents/series/
  exists: ~/storage/series/
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

Uses plugins: [wiki:ModulePreset preset], [wiki:InputRSS RSS], [wiki:FilterSeries10 series], [wiki:OutputDownload download]

[wiki:TheCookBook Back to The Cook Book]