= Deluge =

Downloads content from entry url and loads it into the [http://deluge-torrent.org deluge] bittorrent client.

'''{{{Requirements:}}}'''
Supports Deluge 1.1, 1.2, and 1.3. This will not work if you are running deluge in classic mode, you must switch to running the daemon seperately. If you are running deluged as a different user, on a different box, or with a non-default config directory, (something other than ~/.config/deluge) you will need to specify the user and pass options that you have set up in your deluge [http://dev.deluge-torrent.org/wiki/UserGuide/Authentication auth] file.

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
||content_filename||This can be used to rename the main file inside the torrent. [wiki:Plugins/deluge#ContentRenaming see here]||



== Advanced ==

Some plugins allow [wiki:Plugins/set set:] statements as a subcommand.
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
        movedone: "/media/diskb/TV/%(series_name)s/Season %(series_season)d/"
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

=== Content Renaming* ===
The deluge plugin also supports another advanced feature: content file renaming. This will allow you to change the filename of the main file inside the torrent in deluge. It will only rename a file if it finds that 1 file in the torrent is larger than 90% of the total torrent content. Here is an example configuration:
{{{
series:
  settings:
    groupa:
      set:
        content_filename: "%(series_name)s - S%(series_season)02dE%(series_episode)02d - %(quality)s"
        movedone: /home/user/TV/%(series_name)s/Season %(series_season)d/
  groupa:
    - Show Name
deluge: yes
}}}
This config uses python [wiki:Plugins/set#string-replacement string replacement] notation to rename the file using information from the series parser. If there was a file called {{{Show.Name.9x15.REPACK.720p.HDTV.x264-IMMERSE.[eztv].mkv}}} inside the torrent, it would be renamed to {{{Show Name - S09E15 - 720p.mkv}}} If there is already a file with the new name present in either the downloading folder, or movedone folder, a trailing number will be added to the filename. i.e. {{{Show Name - S09E15 - 720p(2).mkv}}}

Together with the movedone command, this means all TV series will be downloaded to:
{{{
/home/user/TV/Show Name/Seanson #/Show Name - S##E## - Quality.ext
}}}

''* This feature requires Deluge 1.2 or newer and !FlexGet r1227 or newer.''
== Windows Users ==
''(This should be done after you [wiki:InstallWizard/Windows install] !FlexGet)''

The Deluge Windows installer does not install deluge or it's dependencies to the python site-packages folder. This means, in order to get !FlexGet to use the deluge module, you will have to use easy_install to get them there. Go to a command prompt at C:\Program Files\Deluge\Deluge-Python\ (or wherever your deluge install is) and typed 'easy_install deluge-1.3.0_rc1-py2.6.egg' obviously, this is for 1.3 rc1, adjust the command for whatever version you are using. Remember you also need to install dependencies too. If you want to see what dependency is failing try to 'from deluge.ui.client import client' in a python shell, the resulting error will usually give you a pretty good idea of what you are missing. Install that, then try the import again till it works successfully. Then once you have all the dependencies, try to run flexget again.

Here are a list of dependencies you probably need to install:
 - Twisted, Zope.Interface, and pyopenssl can be found at the [http://twistedmatrix.com/trac/wiki/Downloads twisted download page].
 - pywin32 can be found [http://sourceforge.net/projects/pywin32/files/ here.]
 - pyxdg can be installed using the command 'easy_install !http://www.freedesktop.org/~lanius/pyxdg-0.18.tar.gz' (pyxdg will not be necessary after deluge 1.3rc2) 