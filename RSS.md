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