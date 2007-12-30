= Welcome to !FlexGet Trac =

!FlexGet is a software that main focus is to automate downloading content from various sources. 
Most common usage is downloading .torrent files from RSS-feeds, but you can use it to download 
latest podcasts as well.

!FlexGet is completely modular and all features are actually plugins.

== How easy is it to use? ==

Easy configuration was top priority when designing application. However some basic knowledge 
about regular expression is usually needed for effective usage.

!FlexGet uses [http://en.wikipedia.org/wiki/Yml YML-syntax] in configuration files.

Short example:

{{{
feeds:
  name of some feed:
    rss: http://something.com/rss.xml
    patterns:
      - serie.name
    download: ~/series
}}}

This example would download all (new) .torrent files matching regular expression {{{serie.name}}} .

For more information about what !FlexGet can do, see [wiki:modules modules documentation].

