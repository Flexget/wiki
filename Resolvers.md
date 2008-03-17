= Resolvers =

== What are they for ==

Many RSS-feeds and other sources do not provide URLs directly to a torrent-file, but instead a download page of some site. This makes these feeds almost useless for automating downloading. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== How they work ==

Resolvers are modules that detect if [wiki:Entry entry] URL points to a download page instead of actual content. When such URL is detected resolver will step in modify it so that it points into a content. This is usually archieved by editing URL or by requesting the page and finding the download link from there.

=== Currently supported ===

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova
 * !TorrentSpy

== Not on list? Make your own ==

If you only need to replace some words from URL to make it work almost anyone should be able to do it by using existing modules as starting point.