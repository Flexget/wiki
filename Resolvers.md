= Resolvers =

== What are they for ==

Many RSS-feeds (and other inputs) don't provide URLs directly to a torrent-file, but instead point to a download page in another site. This makes these feeds almost useless for automating downloading in most of the applications. !FlexGet overcomes this by providing clean and easy way to add custom functionality for such sites.

== Role ==

It's important to differentiate resolver from input plugins. Input plugins require configuration and create !FlexGet [wiki:Entry entries] from somewhere external (ie. [wiki:Plugin/rss rss feeds] or [wiki:Plugin/html html pages]). Resolvers work without any configuration and only modify [wiki:Entry entries].

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

=== Custom rewriting with regexp ==

In case the download URL is only slightly different from the download page, you can use [wiki:Plugins/regexp_resolver regexp_resolver] plugin to get proper download url.

== Not on the list? Make your own ==

Use existing resolver as a starting point, it should be quite easy if you have any programming experience.