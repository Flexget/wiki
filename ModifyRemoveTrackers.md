= Remove Trackers =

Removes trackers from torrent files using regexp matching.

Configuration example:

{{{
remove_trackers:
  - .*moviex.*
}}}

This will remove all trackers that contain text moviex in their url.
TIP: You can use [wiki:GlobalSection global section] in configuration to make this enabled on all feeds.