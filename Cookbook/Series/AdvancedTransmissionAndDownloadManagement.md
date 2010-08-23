
= config.yml > presets: =
{{{
presets:
  global:
    # configuration of email parameters
    # -> each feed will send an email with the accepted entries
    # -> can be disabled per feed with email: active: False
    email:
      active: True
      from: <from_email_address>
      to: <to_email_address>
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_login: true
      smtp_username: <username>
      smtp_password: <password>
      smtp_tls: true
  # configuration of transmission parameters
  # -> each accepted feed item will be piped to transmission
  # -> if you will connect to a remote host you must use svn-rev: r1370 (trac# 654)
  transmission:
    transmissionrpc:
      host: <host or ip address>
      port: 9091
      removewhendone: True
      username: <username>
      password: <password>
      ratio: -1.0
      addpaused: No
  tv:
    # configuration of adv_exec parameters
    # -> I've got multiple volumes with tv series in my setup and not all of them are always
    # -> connected or mounted to my system, but I will check them with the plugin exists_series.
    # -> So I used the plugin adv_exec to execute a shell script which manages my volumes.
    # -> The script creates symbolic links for each "real" volume and creates "fake" folders 
    # -> for each missed volume in ~/.flexget/exists_series/folder[0|1|2|...]
    adv_exec:
      on_start:
        event: /Users/flexget/.flexget/manage_exists_series.sh
    # configuration of exists_series parameter
    # -> check each accepted entry in the feed against these folders of series
    # -> if the item exists in one of the folders, it wouldn't be dowloaded again.
    exists_series:
      - /Users/flexget/.flexget/exists_series/folder0
      - /Users/flexget/.flexget/exists_series/folder1
      - /Users/flexget/.flexget/exists_series/folder2
    # configuration of series parameters
    # -> this lists represents my series I would automaticly downlaoded via transmission
    series:
      - Caprica
      - Chuck
      - Cougar Town
      - Despreate Housewives
      - Eureka
      - FlashForward
      - Fringe
      - Grey's Anatomy
      - Man vs Wild
      - Persons Unknown
      - Stargate Universe
      - The Big Bang Theory
      - The IT Crowd
      - Two and a Half Men
      - V
      - Warehouse 13
    # configuration of quality parameters
    # -> I don't need the 720p files > 1 GB in size
    # -> so I defined HDTV as my preferred quality
    quality: hdtv
}}}

= config.yml > feeds: =
Thanks to user gazpachoking and his patch in r1367 we can now use [wiki:Plugins/set Plugin/set] to set the path for each entry in feed manage-series and manage-series-remote.

{{{
feeds:
  EZTV:
    rss: <feed url>
    preset:
      - transmission
      - tv
    priority: 10

  BTCHAT_EZTV:
    rss: <feed url>
    preset:
      - transmission
      - tv
    priority: 20

  BTCHAT_VTV:
    rss: <feed url>
    preset:
      - transmission
      - tv
    priority: 30

  SHOWRSS:
    rss: <feed url>
    preset:
      - transmission
      - tv
    priority: 40

  ZOINK:
    # this is a huge html site with a lot of torrents so check this "feed" only every 7th day
    # -> this is only a backup feed. Every feed above should list episodes of my series.
    # -> but sometimes they have trouble with the system (server, dns, etc) and the feed is not reachable
    interval: 7 days
    html:
      url: <html url>
      title_from: url
    preset:
      - transmission
      - tv
    priority: 50
    
# Inspired by the great wiki cookbook entry "Sort Downloads" (http://flexget.com/wiki/Cookbook/SortDownloads)
# I designed some "feeds" that manages my downloaded series on my local machine and on my network storage.
# It will sort the completed torrents by "<series_name>/Season <series_season>/<file>" (remote and local)

  manage-series-remote:
    # use as the feed input a local directory where my series are located
    # TODO: this is a remote folder and it is not always mounted
    #       and listdir exits with an error and the scripts execution stopped
    # -> maybe use a similar solution like in the preset with the custom check script
    listdir:
      - /Volumes/media.video/TV-Series/_complete/
    # the series plugin rejected every item that was seen before
    # so we must disable the builtin seen functions
    disable_builtins: [seen]
    # the same list of series like in the tv preset section
    series:
      - Caprica
      - Chuck
      - Cougar Town
      - Despreate Housewives
      - Eureka
      - FlashForward
      - Fringe
      - Grey's Anatomy
      - Man vs Wild
      - Persons Unknown
      - Stargate Universe
      - The Big Bang Theory
      - The IT Crowd
      - Two and a Half Men
      - V
      - Warehouse 13
    # because of the remote execution we must manipulate the path
    # -> my volumes are locally mounted under /Volumes/...
    # -> and on my remote storage hdd they are located in /share/...
    manipulate:
      location:
        replace:
          regexp: 'Volumes'
          format: 'share'
    # for each accepted and rejected video file we open a ssh connection and move
    # the downloaded file from the completed torrent directory to the destination
    # Please note: you must connect to the remote host without a password!
    #              use a public key instead!
    set:
      path: /share/media.video/TV-Series/%(series_name)s/Season %(series_season)02d
    adv_exec:
      on_output:
        for_rejected: ssh flexget@192.168.1.2 'umask 0000 && mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"'
        for_entries:  ssh flexget@192.168.1.2 'umask 0000 && mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"'
    # please send no email with the result so deactivate this function from the preset
    email:
      active: False

  manage-series:
    # use as the feed input a local directory where my series are located
    listdir:
      - /Users/flexget/Downloads/_Torrents/complete/
    # the series plugin rejected every item that was seen before
    # so we must disable the builtin seen functions
    disable_builtins: [seen]
    # the same list of series like in the tv preset section
    series:
      - Caprica
      - Chuck
      - Cougar Town
      - Despreate Housewives
      - Eureka
      - FlashForward
      - Fringe
      - Grey's Anatomy
      - Man vs Wild
      - Persons Unknown
      - Stargate Universe
      - The Big Bang Theory
      - The IT Crowd
      - Two and a Half Men
      - V
      - Warehouse 13
    set:
      path: /Users/flexget/Movies/Series/%(series_name)s/Season %(series_season)02d
    # for each accepted and rejected video file we open a ssh connection and move
    # the downloaded file from the completed torrent directory to the destination
    adv_exec:
      on_output:
        for_entries:  mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"
        for_rejected: mkdir -p "%(path)s" && mv "%(location)s" "%(path)s/"
    # please send no email with the result so deactivate this function from the preset
    email:
      active: False
}}}

Uses plugins: [wiki:Plugins/preset preset], [wiki:Plugins/email email], [wiki:Plugins/transmissionrpc transmissionrpc], [wiki:Plugins/adv_exec adv_exec], [wiki:Plugins/exists_series exists_series], [wiki:Plugins/series series], [wiki:Plugins/quality quality], [wiki:Plugins/html html], [wiki:Plugins/rss rss], [wiki:Plugins/listdir listdir], [wiki:Plugins/manipulate manipulate]

[wiki:Cookbook Back to The Cookbook]

= helper script: manage_exists_series.sh =
{{{
#!/bin/sh

EXISTS_SERIES="/Users/flexget/.flexget/exists_series"
VOLUMES=(
"/Users/flexget/Movies/Series/"
"/Volumes/media.video/TV-Series/"
"/Volumes/My Book Media/00 Series/"
)

rm -rf "$EXISTS_SERIES/"
mkdir -p "$EXISTS_SERIES/"

for i in ${!VOLUMES[@]}; do
    VOLUME=${VOLUMES[$i]}
    if [ -d "$VOLUME" ]; then
        ln -s "$VOLUME" "$EXISTS_SERIES/folder$i"
    else
        mkdir -p "$EXISTS_SERIES/folder$i"
    fi
done
}}}

[wiki:Cookbook Back to The Cookbook]