## New Wiki!

It's a new wiki! We've migrated from [trac](https://trac.edgewall.org/) to [realms](http://realms.io) for our wiki. There are many improvements, including better mobile support, and live previews while editing. If there were problems with the markdown conversion, feel free to fix them up. If there are any other issue, come find us in chat, so we can work them out.

## Chat and Support

Join us for chat and discussions via [FlexGet @ Gitter](https://gitter.im/Flexget/Flexget) or [FlexGet @ Freenode](http://webchat.freenode.net/?channels=#flexget)

For support and help use the [Flexget Forums](http://discuss.flexget.com)

For bugs open a [Github Issue](https://github.com/Flexget/Flexget/issues)

As we are always trying to update and expand the features of FlexGet, please refer to **[UpgradeActions](/UpgradeActions)** for **relevant information** and **configuration changes** before upgrading your installation. 


## Important pages
 * **[Installation guide](/Install)**
   * [Upgrading](/Upgrade)
     * [Configuration changes](/UpgradeActions)
 * **[Configuration](/Configuration)**
   * [Common pitfalls](/PitFalls)
 * **[The Cookbook](/Cookbook)**
 * **[Developers](/Developers)**
 * **[Plugins](/Plugins)**
 * **[Forum](http://discuss.flexget.com)**
 * **[Change Log](/ChangeLog)**


## Description
FlexGet is a multipurpose automation tool for content like torrents, nzbs, podcasts, comics, series, movies, etc. It can use different kinds of sources like [RSS-feeds](/Plugins/rss), [html pages](/Plugins/html), [csv files](/Plugins/csv), search engines and there are even plugins for sites that do not provide any kind of useful feeds.

There are numerous [plugins](/Plugins) that allow utilizing FlexGet in interesting ways and more are being added continuously.

FlexGet is extremely useful in conjunction with applications which have [watch directory](/WatchDirectory) support or provide interface for external utilities like FlexGet.


## Feature highlights

<ul id="features">
  <li>
    <h4>Daemon Mode</h4>
    <p>
       You can now run FlexGet in <a href="http://flexget.com/wiki/Daemon">daemon mode</a>, and handle scheduling directly in your FlexGet config. Traditional cron scheduling is also supported.
    </p>
  </li>
  <li>
    <h4>Usenet clients</h4>
    <p>
       Integrates with <a href="http://sabnzbd.org/">SABnzbd</a>, and <a href="http://nzbget.sourceforge.net/">nzbget</a> directly, and others via watchdirs.
    </p>
  </li>
  <li>
    <h4>Torrent clients</h4>
    <p>
       Integrates with <a href="http://deluge-torrent.org/">Deluge</a>, <a href="http://www.transmissionbt.com/">transmission</a>, and uTorrent directly, and other clients like rTorrent via watchdirs.
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
    <h4>Site Integration</h4>
    <p>
       Manage and track your series and/or movies directly from <a href="http://trakt.tv/">trakt.tv</a>, <a href="http://thetvdb.com">thetvdb.com</a> or <a href="http://imdb.com">imdb.com</a>.
    </p>
  </li>
  <li>
    <h4>URL rewriting</h4>
    <p>
       Grabs download link from supported download pages, utilize search engines. Read <a href="http://flexget.com/wiki/URLRewriters">more details ...</a>
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



## How easy is it to use?
Easy configuration was a high priority when designing the application. If you have ever used command line based application you should be more than qualified. There is also experimental [Web-UI](/Web-UI) coming along (slowly).

FlexGet uses [YAML](http://en.wikipedia.org/wiki/YAML) for configuration. This may be confusing (for new users) at first but don't be scared, FlexGet is equipped with validator that tries to guide you if you make mistakes.

**Configuration example:** 

This is a complete, fully functional, configuration file! You don't need anything more complex than this to get started.

```
tasks:
  task name:
    rss: http://example.com/torrents.xml
    series:
      - pioneer one
      - some series
    download: ~/torrents/series/
```

This example would download new episodes of `pioneer one` and `some series` to `~/series` using [series](/Plugins/series) plugin.

You can find more configuration examples in [The Cookbook](/Cookbook).

For more information about how FlexGet works, check available [plugins](/Plugins) or detailed [configuration](/Configuration).


## Developers wanted
We're seeking new developers for [web interface](/Web-UI). Python, Javascript and jQuery developers are all needed. Join the IRC-channel if you're up for the task.

## Donate
We appreciate any donations towards hosting costs and development of FlexGet.

<a href="https://gratipay.com/flexget"><img src="https://cdn.rawgit.com/gratipay/gratipay-badge/2.3.0/dist/gratipay.svg"></a>