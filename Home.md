= Welcome to !FlexGet Trac =

== Status? ==

'''!FlexGet is not yet in it's prime condition.''' Some features are incomplete. However I haven't encountered a crash in a while. Please drop a ticket if you encounter problems / weird behaviour! Or if you have good ideas. You can also help by improving this poor wiki :).

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

= Introduction =

!FlexGet is a software that automates downloading content (torrent, mp3, etc.) from various 
sources ([wiki:InputRSS RSS], [wiki:InputHtml html], [wiki:InputCSV CSV] and [wiki:Modules#Inputs more]). 

Most common usage is downloading torrent-files from RSS-feeds. Extremely useful in conjunction with [http://libtorrent.rakshasa.no/ rTorrent].

= Features =

 * Download from [wiki:InputRSS RSS], any [wiki:InputHtml html] page, [wiki:InputCSV CSV] or [wiki:InputRlsLog RlsLog]
 * Use [wiki:FilterPatterns regular expression] to match desired content
 * [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
   * Get best quality in specified time frame
 * Choose movies based on [wiki:FilterImdb imdb] ratings and details
 * Modular structure, extend functionality using and writing plugins (see. [wiki:DevelopersGuide developer guide])

== How easy is it to use? ==

Easy configuration was top priority when designing application. However some basic knowledge 
about regular expression is usually needed for effective usage.

!FlexGet uses [http://en.wikipedia.org/wiki/Yml YML-syntax] in configuration file.

'''Short example.''' Note that this is complete, fully functional configuration file!

{{{
feeds:
  feed name:
    rss: http://something.com/rss.xml
    series:
      - serie name
    download: ~/series
}}}

This example would download all (new) .torrent files matching regular expression {{{serie.name}}} .

For more information about how !FlexGet works, continue to [wiki:Configuration configuration] or straight into [wiki:Modules modules] if above configuration example seems clear to you.