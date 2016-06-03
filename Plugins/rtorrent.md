= rTorrent =

This plugin adds URL's directly into rTorrent and can feed in entries from rTorrent.

'''Supports'''

* Protocols XMLRPC, SCGI and Local SCGI
* Dynamically setting the download directory and custom attributes supporting [wiki:Jinja jinja replacement]
* Magnet urls

== Example ==

Add TVShows to rTorrent and set the download directory to /data/downloads/TV/{{ tvdb_series_name }}

{{{
tasks:
  TV:
    rss: http://domain/rss.xml
    accept_all: yes
    rtorrent:
      uri: scgi://localhost:5000
      path: /data/downloads/TV/{{ tvdb_series_name }}
      custom1: TV
}}}


Once downloaded move to another folder. You can obviously expand on this config to auto extract (using the decompress plugin) and rename the files then keep seeding.

{{{
tasks:
  MOVE-COMPLETE:
    from_rtorrent:
      uri: scgi://localhost:5000
    regexp:
      accept_excluding:
        - complete
      from: custom2
    rtorrent:
      action: update
      custom2: complete
      uri: http://192.168.0.20/north
      path: /data/seeding/{{ custom1 }}/{{ tvdb_series_name }}
}}}

== Options ==

'''Common Options'''

||='''Name'''=||='''Info'''=||='''Description'''=||
||uri||Text||rTorrent URI. IE: scgi://localhost:5000, http://localhost:80/RPC2, /home/rtorrent/rtorrent.sock ||
||username||Text||Username when using HTTP for basic auth||
||password||Text||Password when using HTTP for basic auth||
||timeout||Text||Seconds before timeout when connecting to rtorrent||

'''Output specific options'''

||='''Name'''=||='''Info'''=||='''Description'''=||
||mkdir||[Yes|No]||Create the destination folder on the rTorrent server (default: yes)||
||start||[Yes|No]||Automatically start newly added torrent (default: yes)||
||action||[Yes|No]||[add|update|delete] (Default is add)||
||path||Directory||Destination for downloaded file(s). Supports [wiki:Jinja jinja replacement].||
||priority||Text||[off|low|medium|high] Set torrent priority (default off)||
||custom1||Text||Set custom field||
||custom2||Text||Set custom field||
||custom3||Text||Set custom field||
||custom4||Text||Set custom field||
||custom5||Text||Set custom field||

'''Input specific options'''

||='''Name'''=||='''Info'''=||='''Description'''=||
||view||Text||View to use as input (default main)||
||fields||list||specify which fields to get from rtorrent. See below for default fields||

The following entry fields are set by default on input.

- torrent_info_hash
- title
- up_total
- down_total
- down_rate
- is_open
- is_active
- custom1
- custom2
- custom3
- custom4
- custom5
- state
- complete
- bytes_done
- down_rate
- left_bytes
- ratio
- path

You could use theses to fields to action a torrent.. IE: Remove after x ratio and above

{{{
tasks:
  DELETE-RATIO:
    from_rtorrent:
      uri: scgi://localhost:5000
    if:
      - ratio > 2.0: accept
    rtorrent:
      action: delete
      custom2: complete
      uri: http://192.168.0.20/north
}}}