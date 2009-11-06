{{{
#!html
<div id="login_note">For more permissions (edit wiki, browse sources) login with username: <b>flexget</b> password: <b>anon</b></div>
}}}

{{{
#!html
<h1 style="text-align: left; color: red">Join #FlexGet @ Freenode - Discussion and support</h1>
<h4 style="text-align: left; color: #660000">Looking for a cowboy coder armed with sqlalchemy-migrate</h4>
<div style="float: right">

<font size="1" width=20px>Support my pizza addiction :)</font> 
<div style="text-align: center">

<form action="https://www.paypal.com/cgi-bin/webscr" method="post">
<input type="hidden" name="cmd" value="_s-xclick">
<input type="hidden" name="hosted_button_id" value="8984492">
<input type="image" src="https://www.paypal.com/en_US/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!">
<img alt="" border="0" src="https://www.paypal.com/en_US/i/scr/pixel.gif" width="1" height="1">
</form>

</div>
</div>

}}}

=== Documentation ===

 * '''[wiki:Install Installation guide]'''
 * '''[wiki:Configuration]'''
   * [wiki:PitFalls Common pitfalls]
 * '''[wiki:TheCookBook The Cook Book]'''
 * '''[wiki:Plugins Plugins] (1.0.x)'''
 * '''[wiki:Modules Plugins] (0.9.x)'''

[wiki:NeedHelp Having problems? Help is near!]

== Latest releases ==

[[Include(http://download.flexget.com/ui/download.php)]]

'''Note:''' 1.0 / Bleeding Edge is starting to be quite stable and it's quite major overhaul from 0.9.x. Older users might be interested [wiki:MigrateTo10 how to migrate to bleeding edge environment].

[http://download.flexget.com All builds] | [wiki:Subversion Subversion] | [wiki:BleedingEdge Bleeding edge news]

= Introduction =

!FlexGet is a program aimed to automate downloading and/or processing content (podcasts, comics, torrents, etc.) from different sources like [wiki:InputRSS RSS-feeds], [wiki:InputHtml html-pages], various sites etc.

Application is most often used to download files from RSS-feeds and works nicely in that environment, but you can use it for other purposes as well. There are numerous [wiki:Plugins plugins] that allow utilizing !FlexGet in interesting ways and more plugins are being added continuously.

!FlexGet is extremely useful in conjunction with applications which have [wiki:WatchDirectory watch directory] support.

{{{
#!html
<div>

<div class="supported">
<b>BitTorrent</b>
<ul>
  <li><a href="http://libtorrent.rakshasa.no/">rTorrent</a></li>
  <li><a href="http://utorrent.com">uTorrent</a></li>
  <li><a href="http://www.transmissionbt.com/">Transmission</a></li>
  <li><a href="http://deluge-torrent.org/">Deluge</a>*</li>
</ul>
</div>

<div class="supported">
<b>Usenet</b>
<ul>
  <li><a href="http://nzbget.sourceforge.net/">nzbget</a></li>
  <li><a href="http://www.sabnzbd.org/">sabnzb</a>*</li>
  <li><a href="http://www.hellanzb.com">hellanzb</a></li>
</ul>
</div>

<div class="clearing">
</div>

<sup>* = supported by plugins</sup>

}}}

'''!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).'''[[BR]]

= Features =

 * Process from any [wiki:Plugin/rss RSS] feed, [wiki:Plugin/html HTML] page, [wiki:Plugin/csv CSV] file, or from popular sites like [wiki:Plugin/rlslog RlsLog].
 * Automatically choose movies based on [wiki:Plugin/imdb IMDB] ratings and other details
 * Automatically download subtitles for movies from [http://opensubtitles.org opensubtitles.org]
 * Download [wiki:Plugin/series TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
     * Get best quality available in a specified time frame
     * Min / Max quality
     * Get all specified qualities
   * Proper / Repack aware. Downloaded automatically.
 * Use [wiki:Plugin/regexp regular expressions] to match desired content
 * Keeps track of already downloaded content
 * Easy to add site-specific download scripts / URL re-writers. Many sites supported out of the box. See [wiki:Resolvers resolvers].
 * Completely modular, all features are plugins (see. [wiki:DevelopersGuide developer guide] for more information)
 * And much more ...

= How easy is it to use? =

Easy configuration was a high priority when designing the application. If you have ever used command line based application you should be more than qualified.

!FlexGet uses [http://en.wikipedia.org/wiki/YAML YAML] for configuration. This may be confusing (for new users) at first but don't be scared, !FlexGet is equipped with validator that tries to guide you if you make mistakes.

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

This example would download new episodes of {{{series name}}} and {{{another series}}} to {{{~/series}}}.

You can find more configuration examples in [wiki:TheCookBook The Cookbook].

For more information about how !FlexGet works, check available [wiki:Modules plugins] or detailed [wiki:Configuration configuration].

= Help !FlexGet =

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