= Deluge =

Downloads content from entry url and loads it into the [http://deluge-torrent.org deluge] bittorrent client.

'''Example:'''

{{{
deluge:
  path: /media/diska/downloads/
  movedone: /media/diska/tv/
  label: tv
}}}

All options are optional and will default to whatever you have set in duluge.

== Advanced ==

Some modules may set alternative download path for entry.
Here is an example using the series module:

Example with alternative paths:

{{{
series:
  - pattern1
  - pattern2
  - pattern3:
      path: ~/another_location/
deluge:
  path: ~/first_location/
}}}

This results that entries matching patterns 1 and 2 are saved into
~/first_location/ and pattern3 is saved to ~/another_location/.