= Set download path =

Set series download path using the series_name field, instead of specifying a path for each series.

{{{
feeds:
  feed-a:
    rss: http://example.com
    series:
      - foo
      - bar
    download: /series/location/{{series_name}}
}}}

Uses plugins: [wiki:Plugins/rss rss], [wiki:Plugins/series series], [wiki:Plugins/download download]



[wiki:Cookbook Back to The Cookbook]
