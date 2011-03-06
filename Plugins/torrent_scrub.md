= Torrent metafile scrubber =

Removes resume information and other non-standard data from torrent downloads. Note that this resume information prevents the torrent from properly starting in Rtorrent, and is added by ruTorrent users if they incorrectly check the "Fast Resume" option while creating a torrent for uploading.


== Configuration ==

There is only one settings which determines what kind of metadata is removed from torrents:
 torrent_scrub:: One of `off` (almost equivalent to commenting it out), `on` (normal scrubbing), `all` (never use this on fresh downloads, it can modify the info hash), `resume` (just libtorrent fast-resume information), or `rtorrent` (any special Rtorrent metadata).

Rtorrent users should use `rtorrent`, so that incoming torrents never contain keys that modify the client's behaviour.

== Examples ==

To scrub one feed:
{{{
feeds:
  rutorrent-fast-resume-infected-feed:
    torrent_scrub: rtorrent
}}}

If you want to be sure that all feeds are scrubbed, because you can never know, use this:
{{{
presets:
  global:
    torrent_scrub: rtorrent
}}}
