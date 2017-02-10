# Search Plugins
FlexGet provides framework for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [urlrewrite_search](/Plugins/urlrewrite_search) & [discover](/Plugins/discover) plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


## Overview

### Public

| **Keyword** | **Description** |
| --- | --- |
| [divxatope](/Searches/divxatope) | Generates entries from [divxatope.com](http://divxatope.com/) |
| [flexget_archive](/Searches/flexget_archive) | Searches within previously archived entries |
| [isohunt](/Searches/isohunt) | Generates entries from [isohunt.com](http://isohunt.com) |
| [kat](/Searches/kat) | Generate entries from [kat.ph](http://kat.ph) |
| [newtorrents](/Searches/newtorrents) | Generates entries from [newtorrents.info](http://newtorrents.info) |
| [nyaa](/Searches/nyaa) | Generates entries from [nyaa.se](http://nyaa.se/) |
| [piratebay](/Searches/piratebay) | Generates entries from [thepiratebay](http://thepiratebay.gl/) |
| [publichd](/Searches/publichd) | Generates entries from [PublicHD](http://publichd.se/) |
| [rarbg](/Searches/rarbg) | Generates entries from [RarBG](http://rarbg.com/) |
| [search_rss](/Searches/search_rss) | Generates query based rss feeds |
| [torrent411](/Searches/t411) | Generates entries from [t411.me](http://www.t411.me/) |
| [torrentz](/Searches/torrentz) | Generates entries from [torrentz.eu](http://torrentz.eu) |


### Private

| **Keyword** | **Description** |
| --- | --- |
| [btn](/Searches/btn) | Searches torrent site BTN |
| [cpasbien](/Searches/cpasbien) | Generates entries from [cpasbien.pw](http://www.cpasbien.pw/) |
| [freshon](/Searches/freshon) | Generates entries from [freshon.tv](http://freshon.tv) |
| [iptorrents](/Searches/iptorrents) | Generates entries from [iptorrents.com](http://iptorrents.com) |
| [newznab](/Searches/urlrewrite_newznab) | Generates entries from [newznab.com](http://newznab.com) |
| [ptn](/Searches/ptn) | Searches torrent site PtN |
| [morethantv](/Searches/morethantv) | Generates entries from [morethan.tv](http://morethan.tv) (mtv) |
| [sceneaccess](/Searches/sceneaccess) | Searches torrent site sceneaccess |
|[torrentday](/Searches/torrentday)|Generates entries from torrentday.com
| [torrentshack](/Searches/torrentshack) | Searches torrent site torrentshack |
| [torrentleech](/Searches/torrentleech) | Generates entries from [torrentleech.org](http://torrentleech.org/) |
|[fuzer](/Searches/fuzer) | Searches torrent site Fuzer


You can always get an up to date overview of the available search plugins by using the command line with command 'flexget plugins --group search', and documentation for a plugin can be obtained with 'flexget doc <plugin-name>'.

### Example 

```bash
flexget plugins --interface search
┌─────────────────┬────────────┬───────┐
│ Keyword         │ Phases     │ Flags │
├─────────────────┼────────────┼───────┤
│ 1337x           │            │ doc   │
│ alpharatio      │            │ doc   │
│ btn             │            │       │
│ cpasbien        │            │       │
│ divxatope       │            │ doc   │
│ extratorrent    │            │ doc   │
│ flexget_archive │            │ doc   │
│ fuzer           │            │       │
│ horriblesubs    │ input(128) │ doc   │
│ iptorrents      │            │ doc   │
│ limetorrents    │            │ doc   │
│ morethantv      │            │ doc   │
│ newtorrents     │            │ doc   │
│ newznab         │            │ doc   │
│ nyaa            │            │ doc   │
│ piratebay       │            │ doc   │
│ ptn             │            │       │
│ rarbg           │            │ doc   │
│ sceneaccess     │            │ doc   │
│ search_rss      │            │ doc   │
│ t411            │ input(128) │ doc   │
│ torrent411      │            │ doc   │
│ torrentleech    │            │ doc   │
│ torrentshack    │            │ doc   │
└─────────────────┴────────────┴───────┘
-------------------------------------------------------------------------------
```