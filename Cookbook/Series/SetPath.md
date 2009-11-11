= Set download path =

Set series download path globally with set plugin, instead of specifying a path for each series.

{{{
feeds:
  feed-a:
    rss: http://example.com
    series:
      - foo
      - bar
    set:
      path: /series/location/%(series_name)s
    download: /location/for/rest/
}}}

Uses plugins: [wiki:Plugins/rss rss], [wiki:Plugins/series series], [wiki:Plugins/set set], [wiki:Plugins/download download]

[wiki:Cookbook Back to The Cookbook]
