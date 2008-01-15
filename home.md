= Welcome to !FlexGet Trac =

== Status? ==

!FlexGet is not yet in it's prime condition. Some features are incomplete and application is under constant changes and improvements. It should however work mostly, so feel free to test it out .. please drop a ticket if you encounter problems!

== Quick access ==

 * [wiki:WikiStart Introduction]
 * [wiki:Install Installation and running]
   * [wiki:Install#Download Download]
 * [wiki:modules Modules]
   * [wiki:Entry entries]
 * [wiki:Configuration]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Tips and Tricks]

= Introduction =

!FlexGet is a software that automates downloading content (.torrent, .mp3, etc.) from various 
sources ([wiki:InputRSS RSS], [wiki:InputHtml html], [wiki:InputCSV CSV], etc). 

Most common usage is downloading .torrent files from RSS-feeds. Extremely useful in conjunction with [http://libtorrent.rakshasa.no/ rTorrent].

!FlexGet is built as modular as possible, it should be easy to extend even with minimal python experience (see [wiki:DevelopersGuide developers guide]).

== How easy is it to use? ==

Easy configuration was top priority when designing application. However some basic knowledge 
about regular expression is usually needed for effective usage. At least until [wiki:FilterSeries series] filter is implemented.

!FlexGet uses [http://en.wikipedia.org/wiki/Yml YML-syntax] in configuration file.

'''Short example, complete configuration file for a single rss-feed:'''

{{{
feeds:
  feed name:
    rss: http://something.com/rss.xml
    patterns:
      - serie.name
    download: ~/series
}}}

This example would download all (new) .torrent files matching regular expression {{{serie.name}}} .

For more information about how !FlexGet works, continue to [wiki:modules module documentation].
