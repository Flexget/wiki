{{{
#!html
<h2 style="text-align: left; color: #000">Join <a href="http://webchat.freenode.net/?channels=#flexget">#FlexGet @ Freenode</a> for discussion and support</font></h2>
}}}

Submit your logo ideas [wiki:LogoContest here]!

== Feature highlights ==

{{{
#!html
<ul id="features">
  <li>
    <h4>Usenet clients</h4>
    <p>
       Integrates with <a href="http://sabnzbd.org/">SABnzbd</a>, and <a href="http://nzbget.sourceforge.net/">nzbget</a> directly, and others via watchdirs.
    </p>
  </li>
  <li>
    <h4>Torrent clients</h4>
    <p>
       Integrates with <a href="http://deluge-torrent.org/">Deluge</a>, and <a href="http://www.transmissionbt.com/">transmission</a> directly, and other clients like rTorrent and uTorrent via watchdirs.
    </p>
  </li>
  <li>
    <h4>Movies</h4>
    <p>
       Internal movie queue. Automatic searching. Grab all movies which match predefined imdb and/or rotten tomatoes rules (score, year, etc).
    </p>
  </li>
  <li>
    <h4>Series</h4>
    <p>
      Very comprehensive series support which supports almost everything imaginable. Read <a href="http://flexget.com/wiki/Plugins/series">more details ...</a>
    </p>
  </li>
  <li>
    <h4>trakt.tv</h4>
    <p>
       Manage and track your series directly from <a href="http://trakt.tv/">trakt.tv</a>.
    </p>
  </li>
  <li>
    <h4>thetvdb.com</h4>
    <p>
       Manage and track your series directly from <a href="http://thetvdb.com">thetvdb.com</a>. Use the banners, art and information with FlexGet.
    </p>
  </li>
  <li>
    <h4>Content and client agnostic</h4>
    <p>
       Not built for any specific client or purpose. Use FlexGet to automate all kinds of content processing.
    </p>
  </li>
</ul>
<div style="clear:left;"/>
}}}

== Description ==

!FlexGet is a multipurpose automation tool for content like torrents, nzbs, podcasts, comics, series, movies, etc. It can use different kinds of sources like [wiki:Plugins/rss RSS-feeds], [wiki:Plugins/html html pages], [wiki:Plugins/csv csv files], search engines and there are even plugins for sites that do not provide any kind of useful feeds.

There are numerous [wiki:Plugins plugins] that allow utilizing !FlexGet in interesting ways and more are being added continuously.

!FlexGet is extremely useful in conjunction with applications which have [wiki:WatchDirectory watch directory] support or provide interface for external utilities like !FlexGet.


== How easy is it to use? ==

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

== Developers wanted ==

We're seeking new developers for [wiki:Web-UI web interface]. Python, Javascript and jQuery developers are all needed. Join the IRC-channel if you're up for the task.

== Important wiki pages ==

 * '''[wiki:Install Installation guide]'''
   * [wiki:Upgrade Upgrading]
   * [wiki:Download Manual Download]
 * '''[wiki:Configuration]'''
   * [wiki:PitFalls Common pitfalls]
 * '''[wiki:Cookbook The Cookbook]'''
 * '''[wiki:Developers Developers]'''
 * '''[wiki:Plugins Plugins]'''
