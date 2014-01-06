= Make download RSS =

This will produce rss-feed containing all matches with direct downloadable urls (resolved). This is useful if you wish to hook up !FlexGet with a client that does not have a [wiki:WatchDirectory watch directory] support, or if you wish to perform downloading in a another computer. Only downside is that you need a HTTP server like Apache to host the RSS-feed.

{{{
templates:
  global:
    make_rss:
      link: url
      file: ~/public_html/flexget.rss

feeds:
  some feed:
    regexp:
      accept:
        - example

  another feed:
    series:
      - some series
}}}

Uses plugins: [wiki:Plugins/template template], [wiki:Plugins/make_rss make_rss]

[wiki:Cookbook Back to The Cookbook]

