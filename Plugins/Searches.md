---
title: Plugins/Searches
description: 
published: true
date: 2022-12-12T03:21:15.738Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:39.112Z
---

# Search Plugins
FlexGet provides framework for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [urlrewrite_search](/Plugins/urlrewrite_search) & [discover](/Plugins/discover) plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


### Important!

This list is possibly out of date, it is maintained infrequently.

You can always get an up to date overview of the available search plugins by using the command line with command `flexget plugins --interface search`. Short documentation for a plugin can be obtained with [`flexget doc <plugin-name>`](https://flexget.com/CLI/doc) if included within source file.


### Internal

| **Keyword** | **Description** |
| --- | --- |
| [entry_list](/Plugins/List/entry_list) | Search in an [entry_list](/Plugins/List/entry_list)
| [flexget_archive](/Searches/flexget_archive) | Searches within previously archived entries |

### General

| **Keyword** | **Description** |
| --- | --- |
| [search_rss](/Searches/search_rss) | Generates query based rss feeds |

### Public

| **Keyword** | **Description** |
| --- | --- |
| [1337x.to](/Searches/1337x) | Search [1337x.to](https://1337x.to/) |
| [argenteam](/Searches/argenteam) | Generates entries from [www.argenteam.net](http://www.argenteam.net/) |
| [descargas2020](/Searches/descargas2020) | Generates entries from [descargas2020.com](http://descargas2020.com) |
| [divxatope](/Searches/divxatope) | Generates entries from [divxatope.com](http://divxatope.com/) |
| [eztv](/Plugins/eztv) | Searches EZTV by IMDB ID |
| [gazelle/gazellemusic](/Searches/gazelle) | Generates entries from gazelle-based websites like the now-defunct what.cd |
| [newtorrents](/Searches/newtorrents) | Generates entries from [newtorrents.info](http://newtorrents.info) |
| [nyaa](/Searches/nyaa) | Generates entries from [nyaa.si](http://nyaa.si/) |
| [limetorrents](/Searches/limetorrents) | Generates entries from limetorrents.cc |
| [magnetdl](/Searches/magnetdl) | Generates entries from [magnetdl.com](https://magnetdl.com/) |
| [piratebay](/Searches/piratebay) | Generates entries from [thepiratebay](http://thepiratebay.gl/) |
| [solidtorrents](/Searches/solidtorrents) | Generates entries from [solidtorrents](http://solidtorrents.net/) |

### Private

| **Keyword** | **Description** |
| --- | --- |
| [awesomehd](/Searches/awesomehd) | Searches torrent site AwesomeHD |
| [btn](/Searches/btn) | Searches torrent site BTN |
| [cpasbien](/Searches/cpasbien) | Generates entries from [cpasbien.pw](http://www.cpasbien.pw/) |
| [filelist](/Searches/filelist) | Generates entries from [filelist.ro](https://filelist.ro) |
| [fuzer](/Searches/fuzer) | Searches torrent site [Fuzer](https://www.fuzer.me/) |
| [iptorrents](/Searches/iptorrents) | Generates entries from [iptorrents.com](http://iptorrents.com) |
| [morethantv](/Searches/morethantv) | Generates entries from [morethan.tv](http://morethan.tv) (mtv) |
| [newznab](/Searches/urlrewrite_newznab) | Generates entries from [newznab.com](http://newznab.com) |
| [notwhatcd](/Searches/gazelle) | Generates entries from [NWCD](https://notwhat.cd/) |
| [passthepopcorn](/Searches/passthepopcorn) | Searches torrent site PassThePopcorn |
| [ptn](/Searches/ptn) | Searches torrent site PtN |
| [redacted](/Searches/gazelle) | Generates entries from [RED](https://redacted.ch/) |
| [torrentday](/Searches/torrentday)|Generates entries from torrentday.com
| [torrentleech](/Searches/torrentleech) | Generates entries from [torrentleech.org](http://torrentleech.org/) |

