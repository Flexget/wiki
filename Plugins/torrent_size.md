= Torrent size =

'''Removed in r1202, replaced by [wiki:Plugins/content_size content_size]'''

[[BR]]
[[BR]]
[[BR]]

Reject torrents based on size. As this plugin only '''Rejects''', you need to accept entries with some other filter (ie. [wiki:Plugins/accept_all accept_all], [wiki:Plugins/series series] etc.)

=== Example: ===

{{{
torrent_size:
  min: 12
  max: 1200
}}}

Size is given in MB
