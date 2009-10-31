= Output RSS =

Write RSS containing succeeded (downloaded) entries.

'''Example:'''

{{{
make_rss: ~/public_html/flexget.rss
}}}

You may write into same file in multiple feeds.

'''Example:'''

{{{
my-feed-A:
  make_rss: ~/public_html/series.rss
  .
  .
my-feed-B:
  make_rss: ~/public_html/series.rss
  .
  .
}}}

With this example file {{{series.rss}}} would contain succeeded
entries from both feeds.

Tip: use [wiki:GlobalSection global section] to make RSS of every feed without need to configure them individually.

'''Example:'''

{{{
global:
  make_rss: ~/public_html/flexget.rss

feeds:
  my-feed-A:
    .
    .
  my-feed-B:
    .
    .
}}}