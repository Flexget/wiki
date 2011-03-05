= Remove Trackers =

Removes trackers from torrent files using regexp matching. Also works on magnet urls.

=== Example ===

{{{
remove_trackers:
  - moviex
}}}

This will remove all trackers that contain text moviex in their url.[[BR]]
TIP: You can use [wiki:Plugins/preset global preset] in configuration to make this enabled on all feeds.