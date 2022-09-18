---
title: uTorrent
description: 
published: true
date: 2022-09-18T05:16:35.188Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:09.954Z
---

## uTorrent example

<h1 style="color: red">
 Notice
</h1>


  This recipe should not be needed now that there is a native [utorrent](/Plugins/utorrent) plugin.

This is an example how to use uTorrent with flexget and take advantage of dynamic folders at Windows 7. This is not necessary the right and definitive way to configure uTorrent, but it's a working example. Guide assumes torrents are fetched via RSS and user wants to do RSS fetching periodically without need for manual downloading.

## FlexGet configuration
Let's start with config:

```
# You must tell FlexGet to download the torrent file to some directory, so that it can be passed to uTorrent
    download: C:\torrents

    # Download path defined here can be used later as {{ut_path}} variable
    set:
      ut_path: C:\Movies

    ## Output files to utorrent
    # /DIRECTORY takes two arguments:
    # 1. Save path (now set as {{ut_path}} ). pathscrub to delete unacceptable characters.
    # 2. Torrent file path ( set as {{output}} ). pathscrub done by default.
    # Detailed description: http://forum.utorrent.com/viewtopic.php?id=53988&p=1
    exec: C:\Progam Files\uTorrent.exe /DIRECTORY "{{ut_path|pathscrub}}" "{{output}}"
```

This should be fine for flexget. Replace folders according to your system. Check your configuration with flexget --check.

## Windows 7, uTorrent and Scheduled Tasks
Running uTorrent in Windows 7 can be done either in normal desktop GUI mode (utorrent.exe process type Console) or uTorrent can be run as a Service (utorrent.exe process type Service) on the background and can be accessed only via WebUI interface. Both ways should work fine.

# Console mode
1. Create new task at Scheduled Tasks with option "Run only when user is logged on". See attached file.
2. Add trigger e.g. once every hour
3. Add action: "c:\path\to\flexget\flexget-headless.exe" and with argument "--cron"
4. Modify Conditions and Settings anyway you like

This way flexget is run every hour and new torrents are added to existing uTorrent GUI session. Headless version of flexget avoids command prompt pop-up appearing every time flexget is executed. You need to be logged in to Windows.

There is one downside in this method. Utorrent will be brought up every time new torrent is added to utorrent by scheduled flexget tasks. This can't be avoided with /HIDE or /MINIMIZED or Boss key methods. If there's a way to avoid this downside, don't hesitate to update this wiki.

# Service mode
1. Create new task at Scheduled Tasks with option "Run wheter user is logged on or not"
2. Add trigger e.g. once every hour
3. Add action: "c:\path\to\flexget\flexget.exe" and with argument "--cron"
4. Modify Conditions and Settings anyway you like

This way flexget is run every hour and new torrents are added to existing uTorrent background session. Easy way to create background session is to run newly created Scheduled Task rule manually. Before running, remember to enable WebUI access from uTorrent GUI, otherwise you will lose control to uTorrent.

# Example config
```
tasks:
  movies:
    rss: http://some.tracker.feed.com
    
    # Download path defined here can be used later as {{ut_path}} variable
    set:
      ut_path: C:\Movies

    # Download torrents to
    download: 
      path: C:\Movies
      overwrite: yes

    ## Output files two utorrent
    # /DIRECTORY takes to arguments:
    # 1. Save path (now set as {{ut_path}} )
    # 2. Torrent file path ( set as {{output}} )
    # Detailed description: http://forum.utorrent.com/viewtopic.php?id=53988&p=1
    exec: C:\Progam Files\uTorrent.exe /DIRECTORY "{{ut_path|pathscrub}}" "{{output}}"

  tv:
    rss: http://some.other.tracker.com

    #  Get favourite series from thetvdb.com
    #  Again path variable here is used later
    configure_series:
      from: 
        thetvdb_favorites:
          account_id: <my_account_id>
      settings:
        quality: 720p+
        set:
          ut_path: C:\Series\{{series_name}}\Season {{series_season}}\
      
    download: 
      path: C:\torrents\
      overwrite: yes
    
    # Output series to uTorrent
    exec: C:\Progam Files\uTorrent.exe /DIRECTORY "{{ut_path|pathscrub}}" "{{output}}"
    
```
### Attachments
* [keep-active-session-user-logged-on.png](/attachments/Cookbook/uTorrent/keep-active-session-user-logged-on.png)