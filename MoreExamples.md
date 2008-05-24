= Configuration examples =

=== Simple RSS feeds with regular expression matching ===

{{{
feeds:
  some_rss_feed:
    rss: <url>
    patterns:
      - ^match.something
    download: ~/torrents/

  some_other_rss_feed:
    rss: <url>
    patterns:
      - another.match
    download: ~/torrents/
}}}