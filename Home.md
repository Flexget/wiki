{{{
#!html
<h1 style="text-align: left; color: red">Join #FlexGet @ Freenode - Discussion and support</h1>
}}}

== Quick access ==

 * [wiki:Install Installation guide]
 * [wiki:Configuration]
   * [wiki:PitFalls Common pitfalls]
   * [wiki:CookBook The Cook Book]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Advanced Tips and Tricks]
 * '''[wiki:Modules Plugins]'''
 * [wiki:NeedHelp Problems? Help is near!]

= Releases =

[[ListDownloads]]

[http://download.flexget.com All builds] | [wiki:Subversion Subversion]

= Introduction =

!FlexGet is a program aimed to automate downloading or processing content (torrents, podcasts, etc.) from different
sources like [wiki:InputRSS RSS-feeds], [wiki:InputHtml html-pages], various sites and [wiki:Modules#Inputs more].

Application is most often used to download torrents from RSS-feeds and works nicely in that environment, but !FlexGet is no way limited just for that. There are numerous [wiki:Modules plugins] that allows utilizing !FlexGet in interesting ways and more plugins are being added as the application matures.

!FlexGet is extremely useful in conjunction with applications which have [wiki:WatchDirectory watch directory] support.

'''!BitTorrent'''

 * [http://libtorrent.rakshasa.no/ rTorrent] (see: [wiki:CookBook/rtorrent how to])
 * [http://utorrent.com uTorrent]
 * [http://www.transmissionbt.com/ Transmission]
 * [http://deluge-torrent.org/ Deluge]

'''Usenet (NZB)'''

 * [http://nzbget.sourceforge.net/ nzbget]
 * [http://www.sabnzbd.org/ sabnzb]
 * [http://www.hellanzb.com hellanzb]

'''!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).'''[[BR]]
^* = requires thread support, not present on some routers^ 

= Features =

 * Download from any [wiki:InputRSS RSS] feed, [wiki:InputHtml HTML] page, [wiki:InputCSV CSV] file, or from popular sites like [wiki:InputRlsLog RlsLog].
 * Automatically choose movies based on [wiki:FilterImdb IMDB] ratings and other details
 * Automatically download subtitles for movies from [http://opensubtitles.org opensubtitles.org]
 * Download [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware; get best quality release in a specified time frame
 * Use [wiki:FilterPatterns regular expressions] to match desired content
 * Keeps track of already downloaded content
 * Easy to add site-specific download scripts / URL re-writers. Many sites supported out of the box. See [wiki:Resolvers resolvers].
 * Completely modular, all features are plugins (see. [wiki:DevelopersGuide developer guide] for more information)
 * And much more ...

== Future plans ==

 * Internal scheduler (soon), currently relies on external one
 * Web based configuration interface (in distant future)

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

You can find more configuration examples in [wiki:CookBook the cookbook].

For more information about how !FlexGet works, check available [wiki:Modules plugins] or detailed [wiki:Configuration configuration].

= Help !FlexGet =

{{{
#!html
<div id="login_note">To edit wiki you need to login with username: <b>flexget</b> password: <b>anon</b></div>
}}}


 * Improve this wiki
   * Make any general improvements
   * Write good tutorials
   * Request clearing up confusing parts by adding tag ^''[confusing]''^ (wiki syntax: {{{^''[confusing]''^}}})
   * Request more information by adding tag ^''[need more info]''^
 * Submit more creative plugins (must be MIT-license compatible)
   * Tip: Resolvers for unsupported [http://torrentfreak.com/top-10-torrent-sites-of-2008-081228/ popular sites]
 * Enlist as active developer, help is always welcomed!
 * Report errors you encounter
 * Feedback on areas that you find troublesome