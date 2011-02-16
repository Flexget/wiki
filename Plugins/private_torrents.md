= Private Torrents =

Uses private flag in torrent file to determine what to do with private torrents.

'''Syntax:'''

{{{
private_torrents: yes|no
}}}

=== Example ===

{{{
private_torrents: no
}}}

This would reject all torrent entries with private flag.

=== Example ===

{{{
private_torrents: yes
}}}

This would reject all public torrents.

Non-torrent content is not intervened.