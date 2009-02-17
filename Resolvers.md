= Resolvers =

== What are they for ==

Many RSS-feeds (and other inputs) don't provide URLs directly to a torrent-file, but instead point into a download page in another site. This makes these feeds almost useless for automating downloading in most of the applications. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== Role ==

It's important to differentiate resolver from input modules. Input modules require configuration and create !FlexGet [wiki:Entry entries] from somewhere external (ie. [wiki:InputRSS rss feeds] or [wiki:InputHtml html pages]). Resolvers work without any configuration and only modify [wiki:Entry entries].

== How they work ==

Resolvers are modules that detect if any of the [wiki:Entry entries] in a feed point to a download page instead of actual content. When such a [wiki:Entry entry] is detected, the resolver will step in and modify the URL so that it points into the actual desired content. This is usually achieved by editing URL or by requesting the download page and finding the correct download link from there.

=== Currently supported ===

 * !NewTorrents
 * !PirateBay
 * !IsoHunt
 * !BtJunkie
 * !BtChat
 * Mininova
 * Demonoid
 * Redskunk

== Not on the list? Make your own ==

If you only need to replace some words from URL to make it work almost anyone should be able to do it by using existing modules as starting point.