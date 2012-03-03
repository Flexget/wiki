= Transmission =

Passes the url of an entry to Transmission bittorrent client. Can also pass magnet links to Transmission.

This plugin requires the transmissionrpc library. To install it, run:

{{{
easy_install transmissionrpc
}}}

You may be required to upgrade this after upgrading transmission, for that just add `--upgrade` to previous command.

'''Example:'''

{{{
transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
}}}

If you're having authentication issues, see ticket ticket:1066#comment:1 if it helps (feel free to improve this wiki page).

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
||host||Text||Where transmission is listening (default: localhost)||
||port||Number||Connected port (default: 9091)||
||netrc||File||||
||username||Text||||
||password||Text||||
||path||Directory||Destination for downloaded file(s). Supports [wiki:ValueReplacement value replacement].||
||addpaused||[Yes|No]||||
||bandwidthpriority||[-1,0,1]||||
||honourlimits||[Yes|No]||||
||maxconnections||Number||||
||maxupspeed||Number||||
||maxdownspeed||Number||||
||ratio||Decimal||The ratio to stop seeding at (-1 means infinite)||
||removewhendone||[Yes|No]||Removes ALL stopped or incomplete paused Torrents in the Transmission client, not just the ones added in by FlexGet, if the seed ratio is higher than the global upload ratio. (Caution, will remove almost all all non-active torrents!)||
||enabled||[Yes|No]||Plugin enabled (Default: Yes)||

To use all default values use this config form:
{{{
transmission: yes
}}}

== Advanced ==

Transmission plugin will also utilize options from [wiki:Entry entry] fields. This allow more refined configuration per entries.

Here is an example feed using the series plugin:

{{{
series:
  settings:
    720p:
      set:
        path: /media/diska/incomplete/
        label: 720p
    hdtv:
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
transmission:
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