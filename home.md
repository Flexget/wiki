= Welcome to !FlexGet Trac =

{{{
#!html
<h1 style="text-align: center; color: red">FlexGet wants more users. Spread the word!</h1>
}}}

== Quick access ==

 * [wiki:Install Installation guide]
 * [wiki:Configuration]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Advanced Tips and Tricks]
   * [wiki:CookBook Cook Book]
   * [wiki:Parameters Commandline parameters]
 * '''[wiki:Modules Modules]'''
   * [wiki:Entry Entries]
   * [wiki:Resolvers Resolvers]
 * [wiki:NeedHelp Problems? Help is near!]

= Releases =

||'''Release''' (version)||'''Date''' (dd.mm.yyy)||'''Notes'''||
||[http://download.flexget.com/0.9/FlexGet_0.9.2.2.zip FlexGet v0.9.2.2]||02.03.2009||'''Reported to be broken, please wait a while ...'''.[[BR]]v0.9.2 Fixed #213, #212, #208, #207, #201, #182, #203, #99, #103, #188, #192, #193, #196.[[BR]]Also included fixes for FilterSeries settings block and InputRlsLog combined with FilterImdb.||

[http://download.flexget.com All builds] | [wiki:Subversion Subversion]
[[BR]][[BR]]
'''Old users should check out''' [wiki:ReleaseChanges release and subversion changes].
[[BR]]
= Introduction =

!FlexGet is a program aimed to automate downloading content (torrents, podcasts, etc.) from various 
sources like [wiki:InputRSS RSS-feeds], [wiki:InputHtml html-pages], various sites and [wiki:Modules#Inputs more].

It's most often used to download torrent-files from RSS-feeds and works very well in that environment, but there are additional [wiki:Modules modules] for other kind of situations as well.

!FlexGet is extremely useful in conjunction with applications and clients which have [wiki:WatchDirectory watch directory] support.

'''Examples'''

 * [http://libtorrent.rakshasa.no/ rTorrent] - !BitTorrent client
 * [http://www.hellanzb.com hellanzb] - Download from usenet using NZB-files
 * [http://utorrent.com uTorrent] - !BitTorrent client

'''!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).'''[[BR]]
^* = requires thread support, not present on some routers^ 

'''Application is still in active development phase. ''' 
New features are added frequently and whole application is being improved in every area. This may however lead to bugs at sometimes. If you encounter weird behavior please check if updated version is available and if not [wiki:BugReport report it] by using ticket. 

= Features =

 * Download from any [wiki:InputRSS RSS] feed, [wiki:InputHtml HTML] page, [wiki:InputCSV CSV] file, or from popular sites like [wiki:InputRlsLog RlsLog].
 * Automatically choose movies based on [wiki:FilterImdb IMDB] ratings and other details
 * Automatically download subtitles for movies from [http://opensubtitles.org opensubtitles.org]
 * Download [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware; get best quality release in a specified time frame
 * Use [wiki:FilterPatterns regular expressions] to match desired content
 * Easy to add site-specific download scripts. Many sites supported out of the box. See [wiki:Resolvers resolvers].
 * Completely modular, all features are plugins (see. [wiki:DevelopersGuide developer guide] for more information)

== Distant plans ==

 * Internal scheduler, currently relies on external one
 * Web based configuration UI

= How easy is it to use? =

Easy configuration was a high priority when designing the application. However some basic knowledge 
about regular expression is usually needed for effective usage.

!FlexGet uses [http://en.wikipedia.org/wiki/YAML YAML] for configuration. This may be confusing for new users at first but don't be scared, !FlexGet is equipped with validator that tries to guide you if you make mistakes.

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

You can find more configuration examples in [wiki:CookBook cookbook].

For more information about how !FlexGet works, check available [wiki:Modules modules] or detailed [wiki:Configuration configuration].

= Want to help? =

 * Improve this wiki
 * Write and submit more creative modules (must be MIT-license compatible)
   * Tip: Resolvers for unsupported [http://torrentfreak.com/top-10-torrent-sites-of-2008-081228/ popular sites]
 * Enlist as active developer, help is always welcomed!
 * Report errors you encounter
 * Feedback on areas that you find troublesome
