= Magnets =

This plugin will remove any magnet links from the entry urls list, and reject any entries that only have magnet links. 

Since [wiki:Plugins/torrent_cache torrent_cache] is a built-in plugin, this will mean that most entries fall back to a torrent cache link rather than being rejected. 

This is useful if you are using the [wiki:Plugins/download download] plugin as output, or if you are using the 
[wiki:Plugins/content_filter content_filter] or [wiki:Plugins/content_size content_size] plugins, which cannot get the required information from magnets.

=== Usage ===

{{{
magnets: no
}}} 