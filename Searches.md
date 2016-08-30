# Search Plugins
FlexGet provides framework for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [urlrewrite_search](/Plugins/urlrewrite_search) & [discover](/Plugins/discover) plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


## Overview

### Universal

| **Keyword** | **Description** |
| --- | --- |
| [search_rss](/Searches/search_rss) | Generates query based rss feeds |

### Public

| **Keyword** | **Description** |
| --- | --- |
| [1337x](/Searches/1337x) | Generates entries from [1337.to](http://1337x.to/) |
| [divxatope](/Searches/divxatope) | Generates entries from [divxatope.com](http://divxatope.com/) |
| [extratorrent](/Searches/extratorrent) | Generates entries from [extratorrent.cc](http://extratorrent.cc) |
| [flexget_archive](/Searches/flexget_archive) | Searches within previously archived entries |
| [horriblesubs](/Plugins/horriblesubs) | Generate entries from [horriblesubs.info](http://horriblesubs.info) |
| [isohunt](/Searches/isohunt) | Generates entries from [isohunt.com](http://isohunt.com) |
| [newtorrents](/Searches/newtorrents) | Generates entries from [newtorrents.info](http://newtorrents.info) |
| [nyaa](/Searches/nyaa) | Generates entries from [nyaa.se](http://nyaa.se/) |
| [piratebay](/Searches/piratebay) | Generates entries from [thepiratebay](http://thepiratebay.gl/) |
| [publichd](/Searches/publichd) | Generates entries from [PublicHD](http://publichd.se/) |
| [rarbg](/Searches/rarbg) | Generates entries from [RarBG](http://rarbg.com/) |
| [torrent411](/Searches/t411) | Generates entries from [t411.me](http://www.t411.me/) |
| [limetorrents](/Searches/limetorrents) | Generates entries from [limetorrents.cc](http:/www.limetorrents.cc/) |


### Private

| **Keyword** | **Description** |
| --- | --- |
| [alpharatio](/Searches/alpharatio) | Searches torrent site AlphaRatio |
| [btn](/Searches/btn) | Searches torrent site BTN |
| [cpasbien](/Searches/cpasbien) | Generates entries from [cpasbien.pw](http://www.cpasbien.pw/) |
| [freshon](/Searches/freshon) | Generates entries from [freshon.tv](http://freshon.tv) |
| [iptorrents](/Searches/iptorrents) | Generates entries from [iptorrents.com](http://iptorrents.com) |
| [newznab](/Searches/urlrewrite_newznab) | Generates entries from [newznab.com](http://newznab.com) |
| [ptn](/Searches/ptn) | Searches torrent site PtN |
| [morethantv](/Searches/morethantv) | Generates entries from [morethan.tv](http://morethan.tv) (mtv) |
| [sceneaccess](/Searches/sceneaccess) | Searches torrent site sceneaccess |
| [torrentshack](/Searches/torrentshack) | Searches torrent site torrentshack |
| [torrentleech](/Searches/torrentleech) | Generates entries from [torrentleech.org](http://torrentleech.org/) |
| [whatcd](/Searches/whatcd) | Searches torrent site whatcd|
|[fuzer](/Searches/fuzer) | Searches torrent site Fuzer


You can always get an up to date overview of the available search plugins by using the command line with command `flexget plugins --group search`, and minimal documentation for a plugin can be obtained with `flexget doc <plugin>`.

#### Example

```cmd
flexget plugins --group search
-- Supported search plugins: --------------------------------------------------
 search_rss
 piratebay
 newzleech
 flexget_archive
 newtorrents
 torrentz
-------------------------------------------------------------------------------
```