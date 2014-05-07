My config is very basic.

The only thing it consists of is downloading all series in my trakt list in 480p.

I used the site torrentshack for it.


This is also a clear example of how to use set_begin.

set_begin is very useful when using the discover plugin to avoid it from downloading episodes you have already seen.


{{{
# For flexget V1.2.117
# Using trakt to find your series.
# This is with the discover series plugin and just the rss plugin.
# Note that I used torrentshack but you can just as well use any other site for it.
# Also note that I integrated my config to work with deluge as the plugin for this torrent program is the most advanced.

#####################################################
#                                                   #
# templatessssssssssssssssssssssssssssssss          #
#                                                   #
#####################################################
templates:
  all:
# setting the deluge settings
    deluge:
      username: xxxxxxxx
      password: xxxxxxxx
      path: xxxxxxxx
      movedone: xxxxxxxx
# avoiding magnetlinks.. don't know why I have it actually 
    magnets: no
    configure_series:
      settings:
# setting the quality to 480p because the internet here is very slow and 480p is decent quality
        quality: 480p
      from:
# setting the list you have all your series is
        trakt_list:
          username: xxxxxxxx
          api_key: xxxxxxxx
          custom: xxxxxxxx
          strip_dates: yes

# letting the discoverseries plugin know which episode it should start(finding this by the last episode you have seen)
  set_begin:
    trakt_emit:
      username: xxxxxxxx
      password: xxxxxxxx
      api_key: xxxxxxxx
      list: xxxxxxxx 
    accept_all: yes
    set_series_begin: yes
    


#####################################################
#                                                   #
# taskssssssssssssssssssssssssssssssssssss          #
#                                                   #
#####################################################
# The discover task
# This is a way to discover torrent on torrentshack that you missed with the RSS
# I recommend setting a beginning otherwise it will search the complete last season!


tasks:
  discoverseries:
    template: 
      - all
      - set_begin
    discover:
      what:
        - emit_series: yes
      from:
        - torrentshack:
            username: xxxxxxxx
            password: xxxxxxxx
            category: xxxxxxxx


# This is the RSS download task
# Note: I don't use the template set_begin here because only new episodes will appear in the RSS.
# You might want to set it here too if you notice old episodes are getting downloaded too.

  rssseries:
    template: all
    inputs:
      - rss: 'http://torrentshack.net/feeds.php?user=xxxxxxxx&auth=xxxxxxxx&passkey=xxxxxxxx&authkey=xxxxxxxx&feed=torrents&cat=620'



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