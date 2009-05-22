= Deluge =

Downloads content from entry url and loads it into the [http://deluge-torrent.org deluge] bittorrent client.

'''Example:'''

{{{
deluge:
  path: /media/diska/downloads/
  movedone: /media/diska/tv/
  label: tv
  queuetotop: yes
}}}
 * path: the download location
 * movedone: the location files will be moved when torrent finishes
 * label: deluge label
 * queuetotop: if True will move torrent to top of queue when added

All options are optional and will default to whatever you have set in duluge.
If you wish not to set any of the parameters the format is:
{{{
deluge: yes
}}}

== Advanced ==

Some plugins allow set: statements as a subcommand.
The deluge plugin will read any of the normal parameters from the set: command (path, movedone, label, queuetotop)
Here is an example using the series module:

Example with set:

{{{
series:
  group:
    720p:
      set:
        path: /media/diska/incomplete/
        movedone: /media/diska/TV/%(series_name)s/
        label: 720p
    hdtv:
      set:
        path: /media/diskb/incomplete/
        movedone: /media/diskb/TV/%(series_name)s/Season %(series_season)s/
        label: tv
  720p:
    - pattern1
    - pattern2
  hdtv:
    - pattern3
    - pattern4
        set:
          movedone: /media/diskb/otherfolder/
          queuetotop: True
deluge: yes
}}}

The more specific set commands will override the less specific ones (i.e. the set command from pattern4 will override the set values from the hdtv group.