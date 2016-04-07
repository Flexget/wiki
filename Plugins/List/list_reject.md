=== List Reject ===

This plugin is a [wiki:Plugins/List/ list_interface] plugin.

List plugins can be used as negative filters with the `list_reject` plugin:
{{{
rss: some_feed...
list_reject:
  - trakt_list:
      username: traktusername
      list: watchlist
      type: movies
download: /downloads/
}}}
This will reject any entries that match the entries contained within the list plugin.