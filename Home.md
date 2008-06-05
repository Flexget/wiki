= Welcome to !FlexGet Trac =

== Quick access ==

 * [wiki:Install Installation and running]
   * '''[wiki:Install#Download Download]'''
   * [wiki:Parameters Commandline parameters]
 * [wiki:Configuration]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Advanced Tips and Tricks]
 * [wiki:Modules Modules]
   * [wiki:Entry Entries]
   * [wiki:Resolvers Resolvers]
 * [wiki:NeedHelp Problems? Help is near!]

= Introduction =

!FlexGet is a program aimed to automate downloading content (torrents, podcasts, etc.) from various 
sources like [wiki:InputRSS RSS-feeds], [wiki:InputHtml html-pages] and [wiki:Modules#Inputs more].

It's most often used to download torrent-files from RSS-feeds and works very well in that environment, but there are additional [wiki:Modules modules] for other kind of situations as well.

!FlexGet is extremely useful in conjunction with applications and clients which have [wiki:WatchDirectory watch directory] support.

'''Examples'''

 * [http://libtorrent.rakshasa.no/ rTorrent] - !BitTorrent client
 * [http://www.hellanzb.com hellanzb] - Download from usenet using NZB-files

= Features =

 * Download from any [wiki:InputRSS RSS] feed, [wiki:InputHtml HTML] page, [wiki:InputCSV CSV] file, or from sites like [wiki:InputRlsLog RlsLog] and [wiki:InputTVTorrents TVTorrents].
 * Use [wiki:FilterPatterns regular expressions] to match desired content
 * Download [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware; get best quality release in a specified time frame
 * Choose movies based on [wiki:FilterImdb IMDB] ratings and other details
 * Automatically download subtitles for movies from [http://opensubtitles.org opensubtitles.org]
 * Easy to add site-specific download scripts. Many sites supported out of the box. See [wiki:Resolvers resolvers].
 * Completely modular, all features are plugins (see. [wiki:DevelopersGuide developer guide] for more information)

== How easy is it to use? ==

Easy configuration was a top priority when designing the application. However some basic knowledge 
about regular expression is usually needed for effective usage.

!FlexGet uses [http://en.wikipedia.org/wiki/YAML YAML] for configuration.

'''Configuration example:''' 

This is a complete, fully functional, configuration file! You don't need anything more complex than this to get started.

{{{
feeds:
  feed name:
    rss: http://example.com/torrents.xml
    series:
      - series name
      - another series
    download: ~/series
}}}

This example would download all torrents of {{{series name}}} and {{{another series}}} to {{{~/series}}}.

You can find more configuration examples [wiki:MoreExamples here].

For more information about how !FlexGet works, continue to [wiki:Configuration configuration] or [wiki:Modules modules].

== Want to help? ==

 * Improve this wiki
 * Write and submit more creative modules (must be MIT-license compatible)
   * Tip: Resolvers for [http://torrentfreak.com/bittorrent-sites-show-explosive-growth-080322/ popular sites]
 * Report errors you encounter