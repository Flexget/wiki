= Welcome to !FlexGet Trac =

== Quick access ==

 * [wiki:WikiStart Introduction]
 * [wiki:Install Installation and running]
   * '''[wiki:Install#Download Download]'''
   * [wiki:Parameters Commandline parameters]
 * [wiki:Configuration]
   * [wiki:GlobalSection Global Section]
   * [wiki:TipsAndTricks Advanced Tips and Tricks]
 * [wiki:Modules Modules]
   * [wiki:Entry Entries]
   * [wiki:Resolvers Resolvers]
 * [wiki:NeedHelp Having troubles? Help is near]

= Introduction =

!FlexGet is a software aimed to automate downloading content (torrents, podcasts, etc.) from various 
sources like [wiki:InputRSS RSS-feeds], [wiki:InputHtml html-pages] and [wiki:Modules#Inputs more].

It's most often used to download torrent-files from RSS-feeds and works very well in that situation, but there are built-in [wiki:Modules modules] for much more.

!FlexGet is extremely useful in conjunction with applications and clients which have [wiki:WatchDirectory watch directory] support.

'''Examples'''

 * [http://libtorrent.rakshasa.no/ rTorrent] - !BitTorrent client
 * [http://www.hellanzb.com hellanzb] - Download from usenet using NZB-files

= Features =

 * Download from [wiki:InputRSS RSS], any [wiki:InputHtml html] page, [wiki:InputCSV CSV] or [wiki:InputRlsLog RlsLog]
 * Use [wiki:FilterPatterns regular expression] to match desired content
 * Download [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
   * Get best quality in specified time frame
 * Choose movies based on [wiki:FilterImdb imdb] ratings and other details
 * Clean and easy way to add site-specific download scripts. Many sites supported out of the box. See [wiki:Resolvers resolvers].
 * Completely modular, all features are actually plugins (see. [wiki:DevelopersGuide developer guide])

== How easy is it to use? ==

Easy configuration was a top priority when designing the application. However some basic knowledge 
about regular expression is usually needed for effective usage.

!FlexGet uses [http://en.wikipedia.org/wiki/Yml YML-syntax] in configuration file.

'''Short example.''' Note that this is complete, fully functional configuration file! You don't need more complex setup than this to get started.
{{{
feeds:
  feed name:
    rss: http://something.com/rss.xml
    series:
      - series name
    download: ~/series
}}}

This example would download all episodes of {{{series name}}} to {{{~/series}}}.

For more information about how !FlexGet works, continue to [wiki:Configuration configuration] or straight into [wiki:Modules modules] if above configuration example seems clear to you.

== Want to help? ==

 * Improve this wiki
 * Write and submit more creative modules (must be MIT-license compatible)
   * Tip: Resolvers for [http://torrentfreak.com/bittorrent-sites-show-explosive-growth-080322/ popular sites]
 * Report errors you encounter