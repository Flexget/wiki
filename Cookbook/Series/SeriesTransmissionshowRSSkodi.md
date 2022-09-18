---
title: SeriesTransmissionshowRSSkodi
description: 
published: true
date: 2022-09-18T05:21:21.417Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:18.813Z
---

This configuration is to be used with the a website like [showRSS](http://new.showrss.info/) where you choose which series you want to watch.  Flexget will grab all the series every 30 minutes and send them to Transmission to download.  When the download is complete, Flexget is called again to copy and rename all the files in the download directory.  Finally Flexget tells Kodi to update its video library. 


## config.yml
```
tasks:
  # downloading task and remove finished torrents
  # called via cron every 30 minutes. 
  download-showrss:
    rss:
      url: http://showrss.info/user/MYID.rss?magnets=true&namespaces=true&name=clean&quality=null&re=null
    all_series: yes
    transmission: yes
    clean_transmission:
      host: localhost
      port: 9091
      delete_files: yes
      transmission_seed_limits: yes
  # sorting task called on torrent done
  sort-shows:
    filesystem:
      path: /home/htpc/torrent/complete/
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    accept_all: yes
    disable: seen
    regexp:
      reject:
        - sample
    series:
      settings:
        group 1:
          parse_only: yes
      group 1: 
        - Scandal (2012):
            alternate_name: Scandal US
        - Once Upon a Time (2011):
            alternate_name: Once Upon a Time
        - House of Cards (US):
            alternate_name: House of Cards 2013
        - Last Man Standing (2011):
            alternate_name: Last Man Standing US
        - South Park
        - Modern Family
        - The Middle
        - Game of Thrones
        - Homeland
        - Orange Is the New Black
        - The Fall
        - Better Call Saul
        - Luther
        - Silicon Valley
        - Community
        - True Detective
        - Ballers
        - Narcos
        - The X Files
        - Making a Murderer
        - American Crime Story
    thetvdb_lookup: yes
    copy:
      to: /home/htpc/Videos/TV Shows/{{ tvdb_series_name }}/
      filename: '{{ tvdb_series_name }}.{{ tvdb_ep_id }}'
    kodi_library:
      action: scan
      category: video
      url: http://localhost
      username: kodi
      password: secret
      port: 8080
```

## download-showrss task
This configuration (**download-showrss**) grabs all the series based on the website RSS url for your account (replace **MYID** with your account) and sends to a local Transmission.  The same download task will clean up Transmission once seeding is complete.

command:
```
crontab -e
``` 

to run every 30 minutes
```
0,30 * * * * /usr/local/bin/flexget -l /var/log/flexget.log execute --tasks=download-showrss
```

 - [all_series](/Plugins/all_series): The RSS url determines what shows to grab so we grab them all
 - [transmission](/Plugins/transmission): Use the local Transmission service to download and use all defaults
 - [clean_transmission](/Plugins/clean_transmission): Remove torrents that are done downloading/seeding.  The **transmission_seed_limits** option must be set in order for this plugin to work

## sort-shows task
The second task (**sort-shows**) is called when Transmission completes, set in the **script-torrent-done-filename** option.  This task will move and rename downloads and then tell a running Kodi instance to update its library.

file-name:
```
torrent-done.sh
```

content:
```/bin/bash
/usr/local/bin/flexget -l /var/log/flexget.log execute --tasks sort-shows
```

 - [filesystem](/Plugins/filesystem): Go through the directory where Transmission downloads and find video files
 - [accept_all](/Plugins/accept_all): We don't want to reject anything that has been downloaded
 - [disable](/Plugins/disable): Disable the **seen** plugin since we may want to re-download a show manually
 - [regexp](/Plugins/regexp): Ignore video samples
 - [series](/Plugins/series): The series plugin is used to list all of the shows we want to go through.  Since we do not want anything rejected, we have to set the **parse_only** option.  To apply that option to every series we need to create a group and apply the setting to the group.  [all_series](/Plugins/all_series) with **parse_only** did not work for some reason.
 - [thetvdb_lookup](/Plugins/thetvdb_lookup): Look up the file naming so that Kodi with scrape properly
 - [copy](/Plugins/copy): Use copy instead of move so that seeding will work.  [clean_transmission](/Plugins/clean_transmission) will delete the original download
 - [kodi_library](/Plugins/kodi_library): Send a remote command to Kodi to update the video library