= Advanced example =

How to use most of the series plugin features, with preset:

{{{

tv:
  series:
    settings:
      720p:
        timeframe: 12 hours

    720p:
      - house
      - chuck 

    normal:
      - the colbert report

  download: ~/watch/torrent/series/

feeds:
  my-feed-a:
    rss: http://example.com/feed-a.rss
    preset: tv

  my-feed-b:
    rss: http://example.com/feed-b.rss
    preset: tv

}}}