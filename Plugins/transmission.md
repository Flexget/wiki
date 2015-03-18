= Transmission =

Passes the url of an entry to Transmission bittorrent client. Can also pass magnet links to Transmission.

This plugin requires the transmissionrpc library. To install it, run:

{{{
easy_install transmissionrpc
or
pip install  transmissionrpc
}}}

You may be required to upgrade transmissionrpc after upgrading transmission, for that just add `--upgrade` to the previous command.
Newer versions of flexget now depend on transmissionrpc 0.11 or higher.

'''Example:'''

{{{
transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
}}}

If you're having authentication issues, see ticket ticket:1066#comment:1 if it helps (feel free to improve this wiki page). The username and password can be set from the GUI, but if you're using the headless version you must change it in `/home/<user>/.config/transmission-daemon/settings.json`. First stop transmissiond, edit settings.json and enter a password in clear text; it will be overwritten with its hash once transmissiond is started again.

Also make sure that rpc-whitelist isn't preventing flexget from connecting to localhost or whatever IP address it's using. The settings below will permit clients connecting from localhost and 192.168.*.*, assuming they also provide the correct credentials, it will also deny all other IP ranges:

{{{
    ...
    "rpc-whitelist": "127.0.0.1,192.168.*.*",
    "rpc-whitelist-enabled": true,
    ...
}}}

== Transmission-GTK ==
If you are running Ubuntu, or most any modern distribution, chances are great that you have transmission-gtk instead of transmission-daemon. In this case: Open transmission-gtk, go to Edit > Preferences, and navigate to the Remote tab. Check "Allow remote access" and set your username and password. If "Only allow these IP addresses" is checked, be sure to have your IP included. Test the connection by clicking on "Open web client" button. If you can authenticate from the web client, you should have no problems authenticating with your flexget configuration file as follows:
{{{
transmission:
  host: localhost
  port: 9091
  username: myusername
  password: mypassword
}}}

== Options ==

||'''Name'''||'''Info'''||'''Description'''||
||host||Text||Where transmission is listening (default: localhost)||
||port||Number||Connected port (default: 9091)||
||netrc||File||||
||username||Text||||
||password||Text||||
||path||Directory||Destination for downloaded file(s). Supports [wiki:Jinja jinja replacement].||
||addpaused||[Yes|No]||||
||bandwidthpriority||[-1,0,1]||||
||honourlimits||[Yes|No]||||
||maxconnections||Number||||
||maxupspeed||Number||||
||maxdownspeed||Number||||
||ratio||Decimal||The ratio to stop seeding at (-1 means infinite)||
||enabled||[Yes|No]||Plugin enabled (Default: Yes)||
||main_file_only||[Yes|No]||If yes, all files but the main file inside the torrent (> 'main_file_ratio' of total) will be set to 'skip'||
||main_file_ratio||Decimal||When used with 'main_file_only', the main file inside the torrent must be greater than this value (Default: 0.90)||
||include_subs||[Yes|No]||If yes, in addition to the main file, files with subtitle extensions will be downloaded (.srt, .sub, .idx, .ass, .ssa)||
||content_filename||Text||This can be used to rename the main file inside the torrent. [wiki:Plugins/transmission#ContentRenaming see here]||
||rename_like_files||[Yes|No]||If enabled, file patterns matching the main file will be renamed according to 'content_filename'||
||include_files||Pattern [Single|List]||Will include file patterns if they have been excluded by 'main_file_only'. For patterns [wiki:content_filter see here]||
||skip_files||Pattern [Single|List]||Will 'skip' file patterns if main_file_only is not enabled OR the main_file_only requirement isn't met in the torrent. For patterns [wiki:content_filter see here]||

To use all default values use this config form:
{{{
transmission: yes
}}}

== Advanced ==

Transmission plugin will also utilize options from [wiki:Entry entry] fields. This allows more refined configuration per entry field selection.

Here is an example task using the series plugin:

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

After 1.2.34 the removewhendone option does not exists anymore, you can now clean the Transmission queue using the [wiki:clean_transmission clean_transmission] plugin

=== Content Renaming ===

The transmission plugin also supports another advanced feature: content file renaming. This will allow you to change the filename of the main file inside the torrent in transmission. It will only rename a file if it finds that 1 file in the torrent is larger than 90% of the total torrent content. Here is an example configuration:

{{{
templates:
  torrent:
    transmission:
      host: localhost
      port: 9091
      ratio: 4
  tv:
    template: torrent
    thetvdb_lookup: yes
    exists_series:
      - /mnt/storage/Series/{{ tvdb_series_name }}
    series:
      - serie 1
      - serie 2
      - serie 3
    set:
      path: /mnt/storage/Series/{{ tvdb_series_name }}
      main_file_only: yes
      content_filename: "{{ tvdb_series_name }} - {{ tvdb_season }}x{{ tvdb_episode|pad(2) }} - {{ tvdb_ep_name|default('Missing title') }}"
}}}

This config uses [wiki:Plugins/set#Jinja2Templating jinja2] notation to rename the file using information from the series parser.

=== Selective File Downloading ===

The Transmission Plugin also supports selective file downloading using the settings below.

**NOTE:** Due to the way BitTorrent functions, selecting some files to skip_files may not prevent them from downloading. Torrents are transferred in full chunks; these chunks may cover one or more files and may overlap into files you do not wish to download. The result is that small files in size are likely to download, in full, regardless of your settings. This is not a bug, the developers of Transmission may or may not collect this "junk" data in the future thereby changing this result.

**Example:**

{{{
...
  set:
    path: /mnt/storage/Series/{{ tvdb_series_name }}
    main_file_only: yes
    content_filename: "{{ tvdb_series_name }} - {{ tvdb_season }}x{{ tvdb_episode|pad(2) }} - {{ tvdb_ep_name|default('Missing title') }}"
    rename_like_files: yes
    skip_files:
      - '*.nfo'
      - '*.sfv'
      - '*[sS]ample*'
      - '*.txt'
    include_files:
      - '*.txt'
    include_subs: yes
...
}}}

The result of the above settings depend if the main file is found.

If the main file is NOT found it will exclude any file matching the patterns listed in exclude_files.

If a main file IS found any *.txt file will be downloaded.
Because include_subs is set any *.srt, *.sub, *.idx, *.ass, *.ssa will also be downloaded.

Setting include_subs to yes is the same as:
{{{
...
  set:
    include_files:
      - '*.srt'
      - '*.sub'
      - '*.idx'
      - '*.ass'
      - '*.ssa'
...
}}}


**NOTE:** include_files and skip_files will NEVER apply to the same torrent, finding the main file will always use the include_files config and the skip_files config will be used otherwise.

It is not necessary to enable main_file_only if you only wish to use the skip_files config.