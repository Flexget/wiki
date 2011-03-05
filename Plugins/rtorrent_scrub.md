= Rtorrent metafile scrubber =

Removes resume information and other non-standard data from downloads that prevent the torrent from properly starting in Rtorrent.

'''NOT IMPLEMENTED YET'''

If you use this plugin, you '''MUST''' `easy_install pyrocore` as an additional dependency. Follow the [http://code.google.com/p/pyroscope/wiki/QuickStartGuide installation guide] and [http://code.google.com/p/pyroscope/wiki/UserConfiguration configuration instructions] of PyroScope before adding the plugin configuration to FlexGet.

== Configuration ==

There is only one settings which determines what kind of metadata is removed from torrents:
 rtorrent_scrub:: One of `off` (almost equivalent to commenting it out), `on` (normal scrubbing), `all` (never use this on fresh downloads, it can modify the info hash), `resume` (just libtorrent fast-resume information), or `rtorrent` (any rtorrent metadata).

To prevent the typical problems caused by improper uploads of torrents created by ruTorrent, `resume` is the recommended setting.

== Examples ==

{{{
feeds:
  rutorrent-fast-resume-infected-feed:
    rtorrent_scrub: resume
}}}
