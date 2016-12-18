## Download series with transmission (advanced)


**config.yml** - template section:
```
templates:
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
  transmissionrpc:
    transmission:
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
    # -> for each missed volume in ~/.flexget/exists_series/folder[0|1|2|...](/0|1|2|...)
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
    # -> so I defined HDTV <720p as my preferred quality
    quality: hdtv <720p
```

**config.yml** - feeds section:

Thanks to user gazpachoking and his patch in r1367 we can now use [Plugin/set](/Plugins/set) to set the path for each entry in feed manage-series and manage-series-remote.

```
feeds:
  EZTV:
    rss: <feed url>
    template:
      - transmissionrpc
      - tv
    priority: 10

  BTCHAT_EZTV:
    rss: <feed url>
    template:
      - transmissionrpc
      - tv
    priority: 20

  BTCHAT_VTV:
    rss: <feed url>
    template:
      - transmissionrpc
      - tv
    priority: 30

  SHOWRSS:
    rss: <feed url>
    template:
      - transmissionrpc
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
    template:
      - transmissionrpc
      - tv
    priority: 50
    
# Inspired by the great wiki cookbook entry "Sort Downloads" (https://flexget.com/wiki/Cookbook/SortDownloads)
# I designed some "feeds" that manages my downloaded series on my local machine and on my network storage.
# It will sort the completed torrents by "<series_name>/Season <series_season>/<file>" (remote and local)

  manage-series-remote:
    # use as the feed input a local directory where my series are located
    # TODO: this is a remote folder and it is not always mounted
    #       and filesystem exits with an error and the scripts execution stopped
    # -> maybe use a similar solution like in the template with the custom check script
    filesystem:
      - /Volumes/media.video/TV-Series/_complete/
    # the series plugin rejected every item that was seen before
    # so we must disable the builtin seen functions
    disable_builtins: [seen](/seen)
    # the same list of series like in the tv template section
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
      - location:
          replace:
            regexp: 'Volumes'
            format: 'share'
    # for each accepted and rejected video file we open a ssh connection and move
    # the downloaded file from the completed torrent directory to the destination
    # Please note: you must connect to the remote host without a password!
    #              use a public key instead!
    set:
      path: /share/media.video/TV-Series/{{series_name}}/Season {{series_season|pad(2)}}
    adv_exec:
      on_output:
        for_rejected: ssh flexget@192.168.1.2 'umask 0000 && mkdir -p "{{path}}" && mv "{{location}}" "{{path}}/"'
        for_entries:  ssh flexget@192.168.1.2 'umask 0000 && mkdir -p "{{path}}" && mv "{{location}}" "{{path}}/"'
    # please send no email with the result so deactivate this function from the template
    email:
      active: False

  manage-series:
    # use as the feed input a local directory where my series are located
    filesystem:
      - /Users/flexget/Downloads/_Torrents/complete/
    # the series plugin rejected every item that was seen before
    # so we must disable the builtin seen functions
    disable_builtins: [seen](/seen)
    # the same list of series like in the tv template section
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
      path: /Users/flexget/Movies/Series/{{series_name}}/Season {{"%02d"|format(series_season)}}
    # for each accepted and rejected video file we open a ssh connection and move
    # the downloaded file from the completed torrent directory to the destination
    adv_exec:
      on_output:
        for_entries:  mkdir -p "{{path}}" && mv "{{location}}" "{{path}}/"
        for_rejected: mkdir -p "{{path}}" && mv "{{location}}" "{{path}}"
    # please send no email with the result so deactivate this function from the template
    email:
      active: False
```

Uses plugins: [template](/Plugins/template), [email](/Plugins/email), [transmission](/Plugins/transmission), [adv_exec](/Plugins/adv_exec), [exists_series](/Plugins/exists_series), [series](/Plugins/series), [quality](/Plugins/quality), [html](/Plugins/html), [rss](/Plugins/rss), [filesystem](/Plugins/filesystem), [manipulate](/Plugins/manipulate)

[Back to The Cookbook/Series](/Cookbook/Series)

[Back to The Cookbook](/Cookbook)

## referenced helper script(s) in config.yml
**manage_exists_series.sh**:
```/bin/sh

EXISTS_SERIES="/Users/flexget/.flexget/exists_series"
VOLUMES=(
"/Users/flexget/Movies/Series/"
"/Volumes/media.video/TV-Series/"
"/Volumes/My Book Media/00 Series/"
)

rm -rf "$EXISTS_SERIES/"
mkdir -p "$EXISTS_SERIES/"

for i in ${!VOLUMES[@](/@)}; do
    VOLUME=${VOLUMES[$i](/$i)}
    if [ -d "$VOLUME" ]; then
        ln -s "$VOLUME" "$EXISTS_SERIES/folder$i"
    else
        mkdir -p "$EXISTS_SERIES/folder$i"
    fi
done
```

[Back to The Cookbook/Series](/Cookbook/Series)

[Back to The Cookbook](/Cookbook)