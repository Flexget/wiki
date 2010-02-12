= URL Rewriters =

== What are they for ==

Many RSS-feeds (and other inputs) don't provide URLs directly to a torrent-file, but instead point to a download page in another site. This makes these feeds almost useless for automating downloading in most of the applications. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== How they work ==

URL Rewriters are plugins that detect if any of the [wiki:Entry entries] in a feed point to a download page instead of actual content. When such a [wiki:Entry entry] is detected, the rewriter will step in and modify the URL so that it points into the actual desired content. This is usually achieved by editing URL or by requesting the download page and finding the correct download link from there.

=== Currently supported ===

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova
 * Demonoid
 * Redskunk

=== Custom rewriting with regexp ===

In case the download URL is only slightly different from the download page, you can use [wiki:Plugins/urlrewrite urlrewrite] plugin to get proper download url.

== Not on the list? Make your own ==

Use existing rewriter as a starting point, it should be quite easy if you have any programming experience.