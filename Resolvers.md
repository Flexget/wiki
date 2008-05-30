= Resolvers =

== What are they for ==

Many RSS-feeds (or other inputs) do not provide URLs directly to a torrent-file, but instead a download page of some site. This makes these feeds almost useless for automating downloading. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== How they work ==

Resolvers are modules that detect if an [wiki:Entry entry] URL points to a download page instead of actual content. When such an URL is detected, the resolver will step in and modify the URL so that it points to the actual content. This is usually archieved by editing URL or by requesting the page and finding the download link from there.

=== Currently supported ===

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova

== Not on the list? Make your own ==

If you only need to replace some words from URL to make it work almost anyone should be able to do it by using existing modules as starting point.