---
title: rTorrent
description: 
published: true
date: 2022-09-18T05:14:42.498Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:02.181Z
---

## Complete rTorrent example
This is a complete example for hooking up rTorrent with FlexGet for automatic downloads. This setup will download releases automatically and seed them until the given percentage (here 300%) and then stop seeding. This is important to keep the torrent alive but still avoid overloading your connection. If you delete the torrent from rTorrent the incomplete data is deleted and the torrent directory is cleaned.

For this example, we use the following setup:
 * Base directory (all other directories reside here): /srv/torrent
 * Finished downloads: downloaded
 * Torrent watch directory: torrents
 * Incomplete torrents: incomplete
 * Session data: session

You need to manually create these directories.

It can be tricky to get this all to work and it might be a bit complicated, but please try to understand at least a part of it before using it yourself.

### rTorrent setup
This configuration assumes that you have rTorrent 0.8.x. it might work in other versions as well, but there are no guarantees. You can put this to ~/.rtorrentrc.

```
session = /srv/torrent/session

# Default directory to save the downloaded torrents.
directory = /srv/torrent/incomplete


# Watch a directory for new torrents and set the download target path
schedule = watch_directory_1,10,10,"load_start=/srv/torrent/torrent/*.torrent,d.set_custom1=/srv/torrent/downloaded,d.set_custom2=1"

# Stop torrents which have been deleted from watch directory
schedule = untied_directory,10,10,stop_untied=

# Close torrents when diskspace is low.
schedule = low_diskspace,5,60,close_low_diskspace=50M

# Stop torrents when reaching upload ratio in percent,
# when also reaching total upload in bytes, or when
# reaching final upload ratio in percent.
# example: stop at ratio 3.0 with at least 200 MB uploaded, or else ratio 20.0
#ratio usage with rtorrent below 0.8.4
schedule = ratio,60,60,"stop_on_ratio=300,200M,2000"

#ratio usage with rtorrent above 0.8.4
# Enable the default ratio group.
ratio.enable=
# Change the limits, the defaults should be sufficient.
ratio.min.set=300
ratio.max.set=2000
ratio.upload.set=200M
# Changing the command triggered when the ratio is reached.
system.method.set = group.seeding.ratio.command, d.close=, d.erase=


# Save session data
schedule = session_save,240,300,session_save=

# Move finished downloads to downloaded - for rtorrent below 0.8.5/12.5
on_finished = move_complete,"execute=mv,-u,$d.get_base_path=,$d.get_custom1= ;d.set_directory=$d.get_custom1="
on_finished = set_done_var,d.set_custom2=

# Move finished downloads to downloaded - for rtorrent above 0.8.6/12.6
system.method.set_key = event.download.finished,move_complete,"d.set_directory=$d.get_custom1=;execute=mv,-u,$d.get_base_path=,$d.get_custom1="
system.method.set_key = event.download.finished,set_done_var,d.set_custom2=

# remove incomplete downloads from disk that have been deleted from rTorrent - for rtorrent below 0.8.5/12.5
on_erase = rm_incomplete,"branch=d.get_custom2=,\"execute={rm,-rf,--,$d.get_base_path=}\""

# remove incomplete downloads from disk that have been deleted from rTorrent - for rtorrent above 0.8.6/12.6
system.method.set_key = event.download.erased,rm_incomplete,"branch=d.get_custom2=,\"execute={rm,-rf,--,$d.get_base_path=}\""

```

### FlexGet setup
This configuration is just a simple example, see other recipes for more inspiration.

```
tasks:
  debian:
    html: http://cdimage.debian.org/debian-cd/current/i386/bt-dvd/
    regexp:
      accept:
        - torrent
    download: /srv/torrent/torrents
```

### Final steps
You need to setup a proper crontab entries and start rTorrent to make the magic happen. Setting up crontab is done by running the command `crontab -e` and adding this line:

```
23 */2 * * * /path/to/flexget/flexget.py --cron
```

This will cause FlexGet to be run every second hour 23 minutes past the hour (00:23, 02:23, 04:23, 06:23 and so on), to adjust this read the crontab manual. Also please try to understand the effects of your changes and study the [interval](/Plugins/interval) module before you make any changes.

finally you need to start rTorrent:

```
screen -dSm rtorrent rtorrent
```

to attach the screen and check downloads:

```
screen -r rtorrent
```

You are all done, your downloads should start and stop automatically. All that is left for you to do is to make sure that you don't run out of disk space. 

### Further improvements
[torrent_scrub](/Plugins/torrent_scrub) removes resume information from downloads that prevent the torrent from properly starting in rTorrent.
[Plugins/rtorrent_magnet](/Plugins/rtorrent_magnet) allows saving magnet links in rTorrent format.

[Back to The Cookbook](/Cookbook)