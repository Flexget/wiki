= Welcome to !FlexGet Trac =

== Status? ==

'''!FlexGet is not yet in it's prime condition.''' Some features are incomplete and application is under constant changes and improvements. It should however work without too many troubles so try on, but don't expect it to work perfectly on all situations. Please drop a ticket if you encounter problems / weird behaviour! Or if you have good ideas. You can also help by improving this wiki.

== Quick access ==

 * [wiki:WikiStart Introduction]
 * [wiki:Install Installation and running]
   * [wiki:Install#Download Download]
 * [wiki:modules Modules]
   * [wiki:Entry entries]
 * [wiki:Configuration]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Advanced Tips and Tricks]

= Introduction =

!FlexGet is a software that automates downloading content (.torrent, .mp3, etc.) from various 
sources ([wiki:InputRSS RSS], [wiki:InputHtml html], [wiki:InputCSV CSV], etc). 

Most common usage is downloading .torrent files from RSS-feeds. Extremely useful in conjunction with [http://libtorrent.rakshasa.no/ rTorrent].

!FlexGet is built as modular as possible, it should be easy to extend even with minimal python experience (see [wiki:DevelopersGuide developers guide]).

== How easy is it to use? ==

Easy configuration was top priority when designing application. However some basic knowledge 
about regular expression is usually needed for effective usage. At least until [wiki:FilterSeries series] filter is implemented.

!FlexGet uses [http://en.wikipedia.org/wiki/Yml YML-syntax] in configuration file.

'''Short example.''' Note that this complete fully functional configuration file!

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
