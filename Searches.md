# Search Plugins
FlexGet provides framework for querying searches from supported sites. These cannot be used directly in a task, but can be used with the [urlrewrite_search](/Plugins/urlrewrite_search) & [discover](/Plugins/discover) plugins where they act like options for their parent plugins. This page lists these options and gives a brief description of their function.


## Overview

### Internal
| **Keyword** | **Description** |
| --- | --- |
|`entry_list` | Search in an [entry_list](/Plugins/List/entry_list)
| [`flexget_archive`](/Searches/flexget_archive) | Searches within previously archived entries |
### Public

| **Keyword** | **Description** |
| --- | --- |
| [`argenteam`](/Searches/argenteam) | Generates entries from [www.argenteam.net](http://www.argenteam.net/) |
| [`descargas2020`](/Searches/descargas2020) | Generates entries from [descargas2020.com](http://descargas2020.com) |
| [`divxatope`](/Searches/divxatope) | Generates entries from [divxatope.com](http://divxatope.com/) |
| [`newtorrents`](/Searches/newtorrents) | Generates entries from [newtorrents.info](http://newtorrents.info) |
| [`nyaa`](/Searches/nyaa) | Generates entries from [nyaa.si](http://nyaa.si/) |
| [`piratebay`](/Searches/piratebay) | Generates entries from [thepiratebay](http://thepiratebay.gl/) |
| [`rarbg`](/Searches/rarbg) | Generates entries from [RarBG](http://rarbg.com/) |
| [`search_rss`](/Searches/search_rss) | Generates query based rss feeds |
| [`torrentz`](/Searches/torrentz) | Generates entries from [torrentz.eu](http://torrentz.eu)(deprecated) |
| [`gazelle`/`gazellemusic`](/Searches/gazelle) | Generates entries from gazelle-based websites like the now-defunct what.cd |


### Private

| **Keyword** | **Description** |
| --- | --- |
| [`awesomehd`](/Searches/awesomehd) | Searches torrent site AwesomeHD |
| [`btn`](/Searches/btn) | Searches torrent site BTN |
| [`cpasbien`](/Searches/cpasbien) | Generates entries from [cpasbien.pw](http://www.cpasbien.pw/) |
| [`filelist`](/Searches/filelist) | Generates entries from [filelist.ro](https://filelist.ro) |
| [`fuzer`](/Searches/fuzer) | Searches torrent site [Fuzer](https://www.fuzer.me/) |
| [`iptorrents`](/Searches/iptorrents) | Generates entries from [iptorrents.com](http://iptorrents.com) |
| [`morethantv`](/Searches/morethantv) | Generates entries from [morethan.tv](http://morethan.tv) (mtv) |
| [`newznab`](/Searches/urlrewrite_newznab) | Generates entries from [newznab.com](http://newznab.com) |
| [`notwhatcd`](/Searches/gazelle) | Generates entries from [NWCD](https://notwhat.cd/) |
| [`passthepopcorn`](/Searches/passthepopcorn) | Searches torrent site PassThePopcorn |
| [`ptn`](/Searches/ptn) | Searches torrent site PtN |
| [`redacted`](/Searches/gazelle) | Generates entries from [RED](https://redacted.ch/) |
| [`torrentday`](/Searches/torrentday)|Generates entries from torrentday.com
| [`torrentleech`](/Searches/torrentleech) | Generates entries from [torrentleech.org](http://torrentleech.org/) |

You can always get an up to date overview of the available search plugins by using the command line with command `flexget plugins --interface search`, and documentation for a plugin can be obtained with [`flexget doc <plugin-name>`](https://flexget.com/CLI/doc).

### Example 

```bash
flexget plugins --interface search
┌─────────────────┬────────────┬───────┐
│ Keyword         │ Phases     │ Flags │
├─────────────────┼────────────┼───────┤
│ 1337x           │            │ doc   │
│ alpharatio      │            │ doc   │
│ argenteam       │            │ doc   │
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
│ torrentleech    │            │ doc   │
│ torrentshack    │            │ doc   │
└─────────────────┴────────────┴───────┘
-------------------------------------------------------------------------------
```