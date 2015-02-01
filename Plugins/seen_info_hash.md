= Seen_info_hash =

In the rare event where same torrent is downloaded with different title and url this plugin will step in and see its unique fingerprint (info_hash) and reject it.

This plugin is [wiki:Builtin] and needs no configuration, however you can override some default behavior by configuring it explicitly.

=== Local Mode ===
To only consider previously grabbed torrents within the current task you can configure like this:
{{{
seen_info_hash: local
}}}
=== Turning Off ===
To turn off this plugin on a particular task, you can either use the [wiki:Plugins/disable disable] plugin, or configure it like this:
{{{
seen_info_hash: no
}}}