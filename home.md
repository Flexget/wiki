{{{
#!html
<!--
<div id="login_note">For more permissions (edit wiki, browse sources) login with username: <b>flexget</b> password: <b>anon</b></div>
-->
}}}

{{{
#!html
<h1 style="text-align: left; color: #000">Join #FlexGet @ Freenode - Discussion and support. Spread the FlexGet <font style="color: red">&hearts;</font></h1>
}}}

[[Include(http://download.flexget.com/ui/version.php)]]

=== Important pages ===

 * '''[wiki:Install Installation guide]'''
   * [wiki:Upgrade Upgrading]
   * [wiki:Download Manual Download]
 * '''[wiki:Configuration]'''
   * [wiki:PitFalls Common pitfalls]
 * '''[wiki:Cookbook The Cookbook]'''
 * '''[wiki:Developers Developers]'''
 * '''[wiki:Plugins Plugins]'''

[wiki:NeedHelp Having problems? Help is near!]

= Introduction =

!FlexGet is a multipurpose automation tool for content like torrents, nzbs, podcasts, comics, series, movies, etc. !FlexGet is able to handle different kinds of sources like [wiki:Plugins/rss RSS-feeds], [wiki:Plugins/html html pages] and [wiki:Plugins/csv csv files]. There are even some plugins for sites that do not provide any kind of useful feeds.

There are numerous [wiki:Plugins plugins] that allow utilizing !FlexGet in interesting ways and more are being added continuously.

!FlexGet is extremely useful in conjunction with applications which have [wiki:WatchDirectory watch directory] support or provide interface for external utilities like !FlexGet.

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

<div class="supported">
<b>Other</b>
<ul>
  <li><a href="http://pyload.org/">pyLoad</a></li>
</ul>
</div>

<div class="clearing">
</div>

<sup>* = integrates neatly with a plugin</sup>

}}}

'''!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).'''[[BR]]

== Developers wanted ==

We're currently implementing [wiki:Web-UI web interface] to !FlexGet and would love to have more people join the effort! Python, Javascript and jQuery developers are all needed. Join the IRC-channel if you're up for the task.

= Features =

 * Grab from any [wiki:Plugins/rss RSS] feed, [wiki:Plugins/html HTML] page, [wiki:Plugins/csv CSV] file, or from popular sites like [wiki:Plugins/rlslog RlsLog].
 * Filter movies based on [wiki:Plugins/imdb IMDB] ratings and other details, or even by your rating [wiki:Plugins/imdb_rated history].
 * Download [wiki:Plugins/series TV-series]
   * Episode number aware, doesn't download same episode twice
   * Quality aware
     * Get best quality available in a specified time frame
     * Min / Max quality
     * Get all specified qualities
     * Upgrade qualities retrospectively
   * Propers / Repacks are downloaded automatically or within certain given time
 * Modfy torrents real time, [wiki:Plugins/add_trackers add] or [wiki:Plugins/remove_trackers remove] trackers.
 * Filter based on torrent/nzb [wiki:Plugins/content_filter content] or [wiki:Plugins/content_size size].
 * Use [wiki:Plugins/regexp regular expressions] to match desired content
 * Keeps track of already downloaded content
 * Easy to add site-specific download scripts / URL re-writers. Many sites supported out of the box. See [wiki:URLRewriters URLRewriters].
 * Search queued movies or episodes from search sites like piratebay and nzbmatrix (experimental).
 * Completely modular, all features are plugins
 * And much more ...

= How easy is it to use? =

Easy configuration was a high priority when designing the application. If you have ever used command line based application you should be more than qualified. There is also experimental [wiki:Web-UI] coming along.

!FlexGet uses [http://en.wikipedia.org/wiki/YAML YAML] for configuration. This may be confusing (for new users) at first but don't be scared, !FlexGet is equipped with validator that tries to guide you if you make mistakes.

'''Configuration example:''' 

This is a complete, fully functional, configuration file! You don't need anything more complex than this to get started.

{{{
feeds:
  feed name:
    rss: http://example.com/torrents.xml
    series:
      - pioneer one
      - some series
    download: ~/torrents/series/
}}}

This example would download new episodes of `pioneer one` and `some series` to {{{~/series}}} using powerful [wiki:Plugins/series series] plugin.

You can find more configuration examples in [wiki:Cookbook The Cookbook].

For more information about how !FlexGet works, check available [wiki:Plugins plugins] or detailed [wiki:Configuration configuration].

