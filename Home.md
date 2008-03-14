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
 * [wiki:NeedHelp Having troubles, please help me]

= Introduction =

!FlexGet is a piece of software that automates downloading content (torrent, mp3, etc.) from various 
sources ([wiki:InputRSS RSS], [wiki:InputHtml html], [wiki:InputCSV CSV] and [wiki:Modules#Inputs more]). 

Its most common application is downloading torrent-files from RSS-feeds. It is extremely useful in conjunction with [http://libtorrent.rakshasa.no/ rTorrent].

= Features =

 * Download from [wiki:InputRSS RSS], any [wiki:InputHtml html] page, [wiki:InputCSV CSV] or [wiki:InputRlsLog RlsLog]
 * Most RSS-feeds point to download page instead of content rendering them useless for automation. !FlexGet overcomes this by providing [wiki:Resolvers resolvers] for popular sites that figure out actual download address.
 * Use [wiki:FilterPatterns regular expression] to match desired content
 * Download [wiki:FilterSeries TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
   * Get best quality in specified time frame
 * Choose movies based on [wiki:FilterImdb imdb] ratings and other details
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
 * Report any errors you encounter