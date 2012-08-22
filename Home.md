{{{
#!html
<!--
<div id="login_note">For more permissions (edit wiki, browse sources) login with username: <b>flexget</b> password: <b>anon</b></div>
<div style="border: 2px solid red; padding: 0.5em; text-align:center; margin: 0.5em; background: #ffeeee; font-size: 14pt">Due server upgrade, there may be some problems with the Trac.</div>
-->
}}}

{{{
#!html
<h1 style="text-align: left; color: #000">Join <a href="http://webchat.freenode.net/?channels=#flexget">#FlexGet @ Freenode</a> - Discussion and support. Spread the FlexGet <font style="color: red">&hearts;</font></h1>
}}}

= '''{{{We need a logo, submit your ideas!}}}''' [wiki:LogoContest ->]=

=== Important pages ===

 * '''[wiki:Install Installation guide]'''
   * [wiki:Upgrade Upgrading]
   * [wiki:Download Manual Download]
 * '''[wiki:Configuration]'''
   * [wiki:PitFalls Common pitfalls]
 * '''[wiki:Cookbook The Cookbook]'''
 * '''[wiki:Developers Developers]'''
 * '''[wiki:Plugins Plugins]'''

= Introduction =

!FlexGet is a multipurpose automation tool for content like torrents, nzbs, podcasts, comics, series, movies, etc. It can use different kinds of sources like [wiki:Plugins/rss RSS-feeds], [wiki:Plugins/html html pages], [wiki:Plugins/csv csv files], search engines and there are even plugins for sites that do not provide any kind of useful feeds.

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
  <li><a href="http://pyload.org/">pyLoad</a>*</li>
</ul>
</div>

<div class="clearing">
</div>

<sup>* = directly supported via built in plugin</sup>

}}}

!FlexGet is platform independent, all platforms that have python* available are supported (Linux, Windows, OSX, even some routers and NAS boxes).[[BR]]

== Developers wanted ==

We're currently implementing [wiki:Web-UI web interface] to !FlexGet and would love to have more people join the effort! Python, Javascript and jQuery developers are all needed. Join the IRC-channel if you're up for the task.

= Features =

 * Grab from any [wiki:Plugins/rss RSS] feed, [wiki:Plugins/html HTML] page, [wiki:Plugins/csv CSV] file, or from popular sites like [wiki:Plugins/rlslog RlsLog].
 * Filter movies based on [wiki:Plugins/imdb IMDB] ratings and other details, or even by your rating [wiki:Plugins/imdb_rated history].
 * Add movies to queue manually or automatically from any supported input (think imdb watchlist & imdb android / iPhone app).
 * Search for and download movies from your IMDb or trakt.tv watchlist.
 * Very comprehensive [wiki:Plugins/series TV-series] support.
   * Episode number aware, doesn't download same episode twice
   * Quality aware
     * Get best quality available in a specified time frame
     * Min / Max quality, get all specified qualities
     * Upgrade qualities retrospectively
   * Propers / Repacks are downloaded automatically or only within certain given time
   * Can be [wiki:Plugins/import_series configured] to use an external source for shows, such as [wiki:Plugins/trakt_list trakt.tv] and [wiki:Plugins/thetvdb_favorites thetvdb.com favorites]
 * Modify torrents real time, [wiki:Plugins/add_trackers add] or [wiki:Plugins/remove_trackers remove] trackers.
 * Filter based on torrent/nzb [wiki:Plugins/content_filter content] or [wiki:Plugins/content_size size].
 * Use [wiki:Plugins/regexp regular expressions] to match desired content
 * Keeps track of already downloaded content
 * Easy to add site-specific download scripts / URL rewriters. Many sites supported out of the box. See [wiki:URLRewriters URLRewriters].
 * Completely modular, all features are plugins
 * And much more ...

= How easy is it to use? =

Easy configuration was a high priority when designing the application. If you have ever used command line based application you should be more than qualified. There is also experimental [wiki:Web-UI] coming along (slowly).

!FlexGet uses [http://en.wikipedia.org/wiki/YAML YAML] for configuration. This may be confusing (for new users) at first but don't be scared, !FlexGet is equipped with validator that tries to guide you if you make mistakes.

'''Configuration example:''' 

This is a complete, fully functional, configuration file! You don't need anything more complex than this to get started.

{{{
tasks:
  task name:
    rss: http://example.com/torrents.xml
    series:
      - pioneer one
      - some series
    download: ~/torrents/series/
}}}

This example would download new episodes of `pioneer one` and `some series` to {{{~/series}}} using [wiki:Plugins/series series] plugin.

You can find more configuration examples in [wiki:Cookbook The Cookbook].

For more information about how !FlexGet works, check available [wiki:Plugins plugins] or detailed [wiki:Configuration configuration].