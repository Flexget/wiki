= TransmissionRPC =

Passes the url of an entry to Transmission bittorrent client. Can also pass magnet links to Transmission.

This plugin requires the transmissionrpc library. To install it, run:
{{{
easy_install transmissionrpc
}}}

'''Example:'''

{{{
transmissionrpc:
  host: localhost
  port: 9091
  netrc: /home/flexget/.tmnetrc
  username: myusername
  password: mypassword
}}}

== Options ==

||'''Name'''||'''Info'''||
||host||Required||
||port||Required||
||netrc||File, Optional||
||username||Optional||
||password||Optional||
||path||Optional||
||addpaused||[Yes|No], Optional||
||maxconnections||Number, Optional||
||maxupspeed||Number, Optional||
||maxdownspeed||Number, Optional||
||ratio||Decimal, Optional||

== Advanced ==

Some plugins allow set: statements as a subcommand.
The transmissionrpc plugin will read any of the normal parameters from the set: command

Here is an example using the series module:

Example with set:

{{{
series:
  settings:
    720p:
      quality: 720p
      set:
        path: /media/diska/incomplete/
        label: 720p
    hdtv:
      quality: hdtv
      set:
        path: /media/diskb/incomplete/
        label: tv
  720p:
    - name 1
    - name 2
  hdtv:
    - name 3
    - name 4:
        set:
          ratio: 5.0
          addpaused: yes

transmissionrpc:
  host: localhost
  port: 9091
  netrc: /home/flexget/.tmnetrc
  username: myusername
  password: mypassword
}}}

* Note: because this plugin adds torrents using the source urls, it may fail on some private trackers which require the client to set certain login cookies. One solution is to let the download plugin download the torrent, since FlexGet can be configured to send the proper cookies using the [http://flexget.com/wiki/Plugins/headers headers] plugin. Then use the exec plugin to call the `transmission-remote` program to add the torrent. Example:
{{{
exec: transmission-remote -a '%(output)s'
}}}