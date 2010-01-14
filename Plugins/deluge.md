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

== Options ==

All options are optional and will default to whatever you have set in deluge.
If you wish not to set any of the parameters the format is:

{{{
deluge: yes
}}}

'''Options'''

||'''Name'''||'''Description'''||
||host||Deluge host (default ''localhost'')||
||port||Deluge port (default ''58846'')||
||user||Deluged username ''(defaults to automatic client authentication if not specified)''||
||pass||Deluged password ''(defaults to automatic client authentication if not specified)''||
||path||The download location||
||movedone||The location files will be moved when torrent finishes.||
||label||Deluge label||
||queuetotop||If yes will move torrent to top of queue when added, if no will move to bottom.||
||addpaused||If yes, will add the torrents to deluge in the paused state.||
||maxupspeed||Sets the maximum upload speed. Must be specefied as a decimal (i.e. 1.0)||
||maxdownspeed||Sets the maximum download speed.||
||maxconnections||Sets the maximum connections.||
||maxupslots||Sets the maximum upload slots.||
||ratio||Sets the ratio to stop seeding at.||
||removeatratio||If yes, torrent will be removed from deluge when ratio is reached.||
||compact||If yes, will allocate torrent in compact mode.||
||automanaged||If set to false torrents will be added to deluge without the automanaged flag.||



== Advanced ==

Some plugins allow set: statements as a subcommand.
The deluge plugin will read any of the normal parameters from the set: command, except for deluge daemon info (host, port, user, pass.)
Here is an example using the series module:

Example with set:

{{{
series:
  settings:
    720p:
      quality: 720p
      set:
        path: /media/diska/incomplete/
        movedone: "/media/diska/TV/%(series_name)s/"
        label: 720p
    hdtv:
      quality: hdtv
      set:
        path: /media/diskb/incomplete/
        movedone: "/media/diskb/TV/%(series_name)s/Season %(series_season)s/"
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

The more specific set commands will override the less specific ones (i.e. the set command from name 4 will override the set values from the hdtv group.)

== Windows Users ==
The Deluge Windows installer does not install deluge or it's dependencies to the python site-packages folder. This means, in order to get !FlexGet to use the deluge module, you will have to put them there yourself. You can copy the deluge egg from the deluge install folder (default for rc5 would be C:\Program Files\Deluge\Deluge-Python\deluge-1.2.0_rc5_dev-py2.6.egg) to your python site packages folder (default is C:\Python26\Lib\site-packages) Remember you also need to install dependencies too. If you want to see what dependency is failing try to 'import client from deluge.ui.client' in a python shell, the resulting error will usually give you a pretty good idea of what you are missing. Install that, then try the import again till it works successfully. Then once you have all the dependencies, try to run flexget again.
