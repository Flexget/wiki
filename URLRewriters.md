= URL Rewriters =

== What are they for ==

Many RSS-feeds (and other inputs) don't provide URLs directly to a torrent-file, but instead point to a download page, often in a completely another domain. This makes these feeds almost useless for automating downloading in most of the applications. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== How they work ==

Foremost: automatically and in the background!

URL Rewriters are special type of plugins that detect if any of the [wiki:Entry entries] in a feed point to a download page instead of actual content. When such a [wiki:Entry entry] is detected, the rewriter will step in and modify the URL so that it points into the actual desired content. This is usually achieved by editing URL or by requesting the download page and finding the correct download link from there.

URL Rewriters do not need to be configured aside from generic [wiki:Plugins/urlrewrite urlrewrite]. URL rewriting happens automatically in the background for all supported sites.

=== Currently supported ===

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova
 * Demonoid
 * Redskunk
 * Torrentz
 * BakaBT
 * !DeadFrog

=== Custom rewriting with regexp ===

For unsupported sites you can often rewrite by using regexp. 

This works only when URL is only slightly different from the download page, see [wiki:Plugins/urlrewrite urlrewrite] plugin for more information.

== Not on the list? Make your own ==

Use existing rewriter as a starting point, it should be quite easy if you have any programming experience. !DeadFrog rewriter is a good one to make a copy of and start hacking with it. If you make something, please submit new plugin as a ticket attachment so we can include it in the !FlexGet :)