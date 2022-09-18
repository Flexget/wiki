---
title: SeriesTransmissionshowRSS
description: 
published: true
date: 2022-09-18T05:21:17.541Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:14.994Z
---

This configuration is to be used with the a website like [showRSS](http://showrss.karmorra.info/) where you choose which series you want to watch and the Transmission torrent client.

Let's say a new series you fancy comes out and you want to add it to your download list, instead of opening your configuration file and add it manually (while being prone to all sorts of syntax errors) your go to your showRSS account and add it there, this configuration will fetch all the series it finds from your personal feed at showRSS, download them and organise them with the episode name inside the series folder.

Of course this works will other feeds as well, but the sake of demonstration showRSS is used.

```
tasks:
  # downloading task
  download-rss:
    rss: http://showrss.karmorra.info/rss.php?user_id=MYUSERACCOUNTNUMBER
    # fetch all the feed series
    all_series: yes
    # use transmission to download the torrents
    transmission:
      host: localhost
      port: 9091
      username: username
      password: password
  # sorting task
  sort-files:
    find:
      # directory with the files to be sorted
      path: /home/solenoid/Downloads/
      # fetch all avi, mkv and mp4 files, skips the .part files (unfinished torrents)
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    seen: local
    # this is needed for the episode names
    thetvdb_lookup: yes
    all_series:
      # for some reason all_series rejects all episodes here, even with seen: local, so parse_only must be added
      parse_only: yes
    # TVDB doesn't recognise "Adventure Time with Finn and Jake" so you must add such exceptions here manually
    series:
      - Adventure Time
    move:
      # this is where the series will be put
      to: /home/solenoid/TV/{{ tvdb_series_name }}
      # save the file as "Series Name - SxxEyy - Episode Name.ext"
      filename: '{{ tvdb_series_name }} - {{ series_id }} - {{ tvdb_ep_name }}{{ location | pathext }}'
```

For the complete configuration with Transmission refer to [Transmission setup](/Series/SeriesPresetMultipleRSStoTransmission) and use this configuration in *~/.flexget/config.yml* file.


## Alternative simple setup

```
tasks:
  task-a:
    rss: http://showrss.karmorra.info/rss.php?user_id=USERID&hd=2&proper=0
    all_series: yes
    transmission:
      host: localhost
      port: 9091
      username: USERNAME
      password: PASSWORD
      path: /home/xbian/TV/{{series_name}}/Season {{series_season}}
      addpaused: no
```