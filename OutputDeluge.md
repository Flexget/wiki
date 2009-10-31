= Deluge =

Downloads content from entry url and loads it into the [http://deluge-torrent.org deluge] bittorrent client.
Supports Deluge 1.1.x and 1.2.x apis.

'''Example:'''

{{{
deluge:
  path: /media/diska/downloads/
  movedone: /media/diska/tv/
  label: tv
  queuetotop: yes
}}}
 * path: the download location
 * movedone: the location files will be moved when torrent finishes NOTE: There is a bug in versions of deluge before 1.1.8 that prevents this from working.
 * label: deluge label
 * queuetotop: if True will move torrent to top of queue when added

All options are optional and will default to whatever you have set in deluge.
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
  settings:
    720p:
      quality: 720p
      set:
        path: /media/diska/incomplete/
        movedone: /media/diska/TV/%(series_name)s/
        label: 720p
    hdtv:
      quality: hdtv
      set:
        path: /media/diskb/incomplete/
        movedone: /media/diskb/TV/%(series_name)s/Season %(series_season)s/
        label: tv
  720p:
    - name 1
    - name 2
  hdtv:
    - name 3
    - name 4:
        set:
          movedone: /media/diskb/otherfolder/
          queuetotop: yes
deluge: yes
}}}

The more specific set commands will override the less specific ones (i.e. the set command from name 4 will override the set values from the hdtv group.

== Twisted in bleeding edge ==
To install Twisted into bleeding edge, one must install the development version of setuptools, due to a bug in the current stable version:
{{{
$ ~/src/flexget-dev/bin/easy_install setuptools==dev
<snip install output>

$ ~/src/flexget-dev/bin/easy_install twisted
<snip install output>

$
}}}