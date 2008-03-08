= Resolvers =

Resolvers are modules that detect if [wiki:Entry entry] url points to a download page instead of actual content. When such url is detected resolver will step in modify url so that it points into a content. This is usually archieved by editing url or by requesting the page and finding the download link from there.

This approach allows automating RSS-feeds (or any other input) that would normally be useless because any regular tool would just end up retrieving a download page.

Currently supported sites:

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova
 * !TorrentSpy