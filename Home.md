{{{
#!html
<!--
<div id="login_note">For more permissions (edit wiki, browse sources) login with username: <b>flexget</b> password: <b>anon</b></div>
-->
}}}

{{{
#!html
<h1 style="text-align: left; color: #000">Join #FlexGet @ Freenode - Discussion and support. Spread the FlexGet <font style="color: red">&hearts;</font></h1>
<div style="float: right">

<font size="1" width=20px>Support my pizza addiction :)</font> 
<div style="text-align: center">

<div>
<a class="FlattrButton" style="display:none;"
href="http://flexget.com"></a>
</div>

<div>
<form action="https://www.paypal.com/cgi-bin/webscr" method="post">
<input type="hidden" name="cmd" value="_s-xclick">
<input type="hidden" name="hosted_button_id" value="8984492">
<input type="image" src="https://www.paypal.com/en_US/i/btn/btn_donateCC_LG.gif" border="0" name="submit" alt="PayPal - The safer, easier way to pay online!">
<img alt="" border="0" src="https://www.paypal.com/en_US/i/scr/pixel.gif" width="1" height="1">
</form>
</div>

</div>
</div>

}}}

=== Documentation ===

 * '''[wiki:Install Installation guide]'''
   * [wiki:Upgrade Upgrading]
 * '''[wiki:Configuration]'''
   * [wiki:PitFalls Common pitfalls]
 * '''[wiki:Cookbook The Cookbook]'''
 * '''[wiki:Plugins Plugins] (1.0.x)'''

[wiki:NeedHelp Having problems? Help is near!]

== Latest releases ==

[[Include(http://download.flexget.com/ui/download.php)]]

[http://download.flexget.com All builds] | [wiki:Subversion Subversion] | [wiki:UpgradeActions Upgrade actions]

= Introduction =

!FlexGet is a multipurpose automation tool for content like torrents, nzbs, podcasts, comics, etc. !FlexGet is able to handle different kinds of sources like [wiki:Plugins/rss RSS-feeds], [wiki:Plugins/html html pages] and even [wiki:Plugins/csv csv files]. There are even some plugins for sites that do not provide any kind of useful feeds.

There are numerous [wiki:Plugins plugins] that allow utilizing !FlexGet in interesting ways and more are being added continuously.

!FlexGet is extremely useful in conjunction with applications which have [wiki:WatchDirectory watch directory] support.

{{{
#!html
<div>

<div class="supported">
<b>BitTorrent</b>
<ul>
  <li><a href="http://libtorrent.rakshasa.no/">rTorrent</a></li>
  <li><a href="http://utorrent.com">uTorrent</a></li>
  <li><a href="http://www.transmissionbt.com/">Transmission</a>*</li>
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

<sup>* = natively supported by plugins</sup>

}}}

'''!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).'''[[BR]]

= Features =

 * Process from any [wiki:Plugins/rss RSS] feed, [wiki:Plugins/html HTML] page, [wiki:Plugins/csv CSV] file, or from popular sites like [wiki:Plugins/rlslog RlsLog].
 * Filter movies based on [wiki:Plugins/imdb IMDB] ratings and other details, or even by your rating [wiki:Plugins/imdb_rated history].
 * Automatically download subtitles for movies from [http://opensubtitles.org opensubtitles.org] (#227)
 * Download [wiki:Plugins/series TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
     * Get best quality available in a specified time frame
     * Min / Max quality
     * Get all specified qualities
   * Propers / Repacks are downloaded automatically.
 * Use [wiki:Plugins/regexp regular expressions] to match desired content
 * Keeps track of already downloaded content
 * Easy to add site-specific download scripts / URL re-writers. Many sites supported out of the box. See [wiki:URLRewriters URLRewriters].
 * Completely modular, all features are plugins (see. [wiki:Developers developer guide] for more information)
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
    download: ~/torrents/series/
}}}

This example would download new episodes of {{{series name}}} and {{{another series}}} to {{{~/series}}} using powerful [wiki:Plugins/series series] plugin.

You can find more configuration examples in [wiki:Cookbook The Cookbook].

For more information about how !FlexGet works, check available [wiki:Plugins plugins] or detailed [wiki:Configuration configuration].

= Help !FlexGet =

 * Enlist as active developer, help is always welcomed!
 * Improve this wiki
   * Make any general improvements
   * Write good tutorials
   * Request clearing up confusing parts by adding tag ^''[confusing]''^ (wiki syntax: {{{^''[confusing]''^}}})
   * Request more information by adding tag ^''[need more info]''^
 * Submit more creative plugins (must be MIT-license compatible)
   * Tip: Resolvers for unsupported [http://torrentfreak.com/top-10-torrent-sites-of-2008-081228/ popular sites]
 * Report errors you encounter
 * Feedback on areas that you find troublesome

=== Expand stub pages ===

[[ListTagged(stub)]]