= Using download plugin =
This recipe uses the series plugin to download torrents from an rss feed to a specified path.
{{{
tasks:
  task_name:
    rss: http://example.com
    series:
      - Lost
      - Another Show
    download: /path/to/torrents/
}}}

= Using deluge plugin =
This will do the same, but load the torrents into deluge instead of saving them.
{{{
tasks:
  task_name:
    rss: http://example.com
    series:
      - Lost
      - Another Show
    deluge: yes
}}}