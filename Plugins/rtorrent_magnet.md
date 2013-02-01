= rTorrent Magnet URI Handler =

This plugin will scan accepted items that haven't been downloaded for magnet URI's. if a magnet URI is detected, this plugin will process an rtorrent compatible magnet torrent file to the configured output directory.

=== Example ===

Save magnet link to rTorrent watch directory as a file.

{{{
rtorrent_magnet: ~/torrents/
}}}

However, you can also override the path where magnet file is saved per entry basis (just like the download plugin)

=== External Links ===

* Magnet torrent creation is derived from the content at the [http://wiki.rtorrent.org/MagnetUri rTorrent Wiki MagnetUri page].