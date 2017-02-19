# Series recipes
### Good starting points
* [Very basic series configuration](/Cookbook/Series/SimpleSeries)
* [Manage series and multiple feeds easily](/Cookbook/Series/Template)
* [Set torrent client download path from series name](/Cookbook/Series/SetPath)

### More advanced recipes
* [Manage your series from trakt.tv rather than directly in the FlexGet config](/Cookbook/Series/trakt_manager)
* [Have FlexGet search for the episodes you need rather than monitoring an RSS feed](/Cookbook/Series/Search)
* [Get your FlexGet series database started with the files you already have](/Cookbook/Series/SeedDB)
* [Sort Downloads with FlexGet](/Cookbook/Series/Sort)
* [Remove ended shows you have already collected from a trakt list](/Cookbook/Series/CleanTrakt)
* [Set the first episode of series to be downloaded based on your trakt watched (or collected) status.](/Cookbook/Series/TraktBegin)
* [Set deluge options trough series groups](/Cookbook/Series/DelugeMovedone)
* [Advanced example with setting groups and qualities](/Cookbook/Series/Advanced)
* [Advanced deluge/thetvdb config showing many features](/Cookbook/Series/DelugeThetvdbSeries)
* [Download series with transmission (advanced)](/Cookbook/Series/AdvancedTransmissionAndDownloadManagement)
* [Get series premieres with genre filtering](/Cookbook/Series/PremieresGenres)
* [Fix the nzbclub feed to get series](/Cookbook/Urlrewrite/nzbclub)
* [Upload movie/tv collection to trakt.tv](/Cookbook/Movies/TraktUpload)
* [Set category from series name with sabnzbd](/Cookbook/Series/SeriesSabNZBd)
* [Use next-episode.net as input for import_series](/Cookbook/Series/next-episode)
* [Transmission - Single series list in one template from multiple RSS feeds to Transmission with propers, quality, separate path per series](/Cookbook/Series/SeriesPresetMultipleRSStoTransmission)
* [showRSS to Transmission, file copying/renaming from TVDB and updating Kodi](/Cookbook/Series/SeriesTransmissionshowRSSkodi)
* [Transmission with showRSS: manage your series from showRSS website without messing with the configuration file](/Cookbook/Series/SeriesTransmissionshowRSS)
* [Download episodes from a remote PMS by using local PMS as input](/Cookbook/Series/PlexToPlexDownload)
* [Download nzb for series episodes from a newznab website](/Cookbook/Series/DiscoverSeriesWithNewznab)
* [Remove and forget episodes by file extension](/Cookbook/Series/RemoveByExtension)
* [Remove gaps in your series database by searching a folder for episodes you already downloaded](/Cookbook/Series/sync_series)
* [Get notifications about aired episodes that were missed using Trakt lookup](/Cookbook/Series/monitor_episodes)
 
## Resources
*Torrent feeds*

 * http://showrss.info/feeds/all.rss
 * http://eztv.ag/ezrss.xml
 * http://kat.ph/tv/?rss=1
 * http://torrentz.eu/feed?verified&q=tv%20shows
 * http://extratorrent.cc/rss.xml?cid=8

*NZB Feeds*

 * [www.nzbs.org](http://www.nzbs.org/) (See footnote^1^)

**Footnotes**

 1. The RSS URL for **www.nzbs.org** needs authentication data.  
 First you need to [register](http://nzbs.org/user.php?action=register) with the site.  
 Then follow these [instructions](http://nzbs.org/index.php?action=rss).  
 Example: !http://nzbs.org/rss.php?type=1&i=<uid>&h=<hash>&num=100&dl=1  
 Both the **i** and **h** values are required and account-specific.(XXX macro: "BR") 