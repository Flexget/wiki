= Simple Ebook Recipies =

= Using download plugin =
This recipe uses the regexp plugin to download torrents from an rss feed to a specified path.
{{{
feeds:
  feed_name:
    rss: http://example.com
    regexp:
      accept:
        - Some Publisher
        - Some Magazine
    download: /path/to/torrents/
}}}