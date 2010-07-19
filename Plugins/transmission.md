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
  username: myusername
  password: mypassword
}}}

== Options ==

||'''Name'''||'''Info'''||
||host||Optional (default: localhost)||
||port||Number, Optional (default: 9091)||
||netrc||File, Optional||
||username||Optional||
||password||Optional||
||path||Optional||
||addpaused||[Yes|No], Optional||
||maxconnections||Number, Optional||
||maxupspeed||Number, Optional||
||maxdownspeed||Number, Optional||
||ratio||Decimal, Optional (-1 means infinite)||
||removewhendone||Boolean||
||enabled||Boolean, Optional (default: True)||

To use all default values use this config form:
{{{
transmissionrpc: yes
}}}

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
  username: myusername
  password: mypassword
}}}

=== Transmission Tips ===

'''After r1277 you can simply use removewhendone option'''

Transmission annoyingly do not have any way to easily remove completed torrents from it's UI.
Luckily if you have transmission-remote installed you can script it.

Create an executable script named: transmission-cleanup.sh:

{{{
transmission-remote -l  | grep 100% | grep Done | awk '{print $1}' | xargs -n 1 -J % ./transmission-remote -t % -r
}}}

Note: if you transmission is username/password protected add a --auth <user>:<password> to the above calls to transmission-remote.

Add this script to your crontab.