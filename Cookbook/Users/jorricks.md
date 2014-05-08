My config is very basic.

The only thing it consists of is downloading all series in my trakt list in 480p.

I used the site torrentshack for it.


This is also a clear example of how to use set_begin.

set_begin is very useful when using the discover plugin to avoid it from downloading episodes you have already seen.


{{{
# For flexget V1.2.125
# Using trakt to find your series.
# This is with the discover series plugin and just the rss plugin.
# Note that I used torrentshack but you can just as well use any other site for it.
# Also note that I integrated my config to work with deluge as the plugin for this torrent program is the most advanced.
#####################################################
#                                                   #
# templatessssssssssssssssssssssssssssssss          #
#                                                   #
# This is where I set my deluge torrent client
# Set the quality of the series to 480p
# Set to download from trakt
# Start searching only at next episode
#####################################################
templates:
  all:
    deluge:
      username: localclient
      password: xxxxx
      path: xxxx
      movedone: xxx
    configure_series:
      settings:
        quality: 480p
      from:
        trakt_list:
          username: xxxx
          api_key:xxxxx
          custom: Series
          strip_dates: yes
    trakt_emit:
      username: xxx
      password: xxxxxx
      api_key: xxxxx
      list: Series
    set_series_begin: yes

    trakt_emit:
      username: xxxxx
      password: xxxxx
      api_key: xxxxx
      list: Series
    accept_all: yes
    set_series_begin: yes

#####################################################
#                                                   #
# taskssssssssssssssssssssssssssssssssssss          #
#                                                   #
#####################################################
tasks:
  discoverseries:
    template: all
    discover:
      what:
        - emit_series: yes
      from:
        - torrentshack:
            username: xxxxx
            password: xxxxx
            category: TV/x264-SD

  rssseries:
    template: all
    inputs:
      - rss: 'http://torrentshack.net/feeds.php?user=xxxxx&auth=xxxxx&passkey=xxxxxx$


#####################################################
#                                                   #
# Schedulessssssssssssssssssssssssssssssss          #
#                                                   #
#####################################################
schedules:
  - tasks: 'rssseries'
    interval:
      hours: 1
  - tasks: 'discoverseries'
    interval:
      hours: 4
}}}

I will update this page in the future with my home config.