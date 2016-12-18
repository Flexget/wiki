## Flexget 1.2.313 configuration - TV & movies using showRSS and IMDB-watchlist
For this to work you have to setup a few things.

* Setup your favorite torrent-client and have it look in a folder for new torrents. In this configuration I use transmission.(XXX macro: "BR") Read here for installation instructions: [https://flexget.com/wiki/InstallWizard](/https://flexget.com/wiki/InstallWizard)
* Find a good feed for your series. I highly recommend using showRSS [http://showrss.info](/http://showrss.info)
* You have to find your userID at IMDB look at http://www.imdb.com/user/XXXXXXXXXX/ (the XX.. is your IMDB-userID).
* Create a new e-mail with Gmail or use your existing one for e-mailnotifications.(XXX macro: "BR") Template goes into [flexdir](/flexdir)/templates/

The watchlist you specify in this configuration have to be public for FlexGet to read it.

I had to make a small change to the file search_kat.py for the plugin to work as it pointed to the old adress kickass.to

All thanks to user UnNefer for his e-mail-template from his own guide: https://flexget.com/wiki/Cookbook/Users/UnNefer

----

Below is my configuration as of 2015.06.01. Template is located at the bottom of this page to be downloaded.

```
#####################################################################################
#
# KnockiMov FlexGet-configuration
#------------------------------------------------
# Built to work with both movies and series populated with IMDB-watchlist and
# showRSS and automatically send an e-mail with news with what was added
# and/or downloaded with transmission using its watch-folder.
#
#####################################################################################
#
# Templates for easy configuration
#------------------------------------------------
# First we give a global-template that will be owned by all tasks that will be run.
# Remember to change your username, password and your host for transmission.
# For e-mail to work, change sending/recieving e-mail and passord. This uses gMail.
# 
#####################################################################################

templates:
  global:
    # REJECT ANY TORRENT THAT CONTAINS ONE OF THESE
    # WORDS IN BETWEEN A SPACE OR A DOT
    regexp:
      reject:
        - (?i)[ .]webrip[ .]
        - (?i)[ .]cam[ .]
        - (?i)[ .]bdscr[ .]
        - (?i)[ .]dvdscr[ .]
        - (?i)[ .]preair[ .]
        - (?i)[ .]ppvrip[ .]
        - (?i)[ .]r5[ .]
        - (?i)[ .]tc[ .]
        - (?i)[ .]ts[ .]
        - (?i)[ .]ecc[ .]
        - (?i)[ .]avc[ .]
        - (?i)[ .]qebs[ .]
        - (?i)[ .]hdtc[ .]
        - (?i)[ .]hdcam[ .]

    # CLEAN TRANSMISSION SO IT WILL NOT BE CLUTTERED, STOPS
    # SEEDING AFTER A RATIO OF 2 AND THEN CLEANS OUT THE LIST.
    clean_transmission:
      host: [YOURHOST](/YOURHOST)
      port: 9091
      username: [USERNAME](/USERNAME)
      password: [PASSWORD](/PASSWORD)
      min_ratio: 2

    # IF SOMETHING WAS ADDED, DOWNLOADED OR QUEUED
    # SEND AN e-MAIL WITH STATUS TO GIVEN e-MAIL
    email:
      active: True
      from: [E-MAIL](/E-MAIL)@gmail.com
      to: [E-MAIL](/E-MAIL)@gmail.com
      smtp_host: smtp.gmail.com
      smtp_port: 587
      smtp_username: [E-MAIL](/E-MAIL)@gmail.com
      smtp_password: [PASSWORD](/PASSWORD)
      smtp_tls: yes
      template: html-downloaded.template

#####################################################################################
#
# We now give more direct templates for manipulating and assigning how torrents
# will be handled and where to put them. We also seperate series and movies with
# seperate templates for each. This for easy manipulation and adding in new series.
#
#####################################################################################

  tv:
    # WHERE TO FIND TORRENTS. I HIGHLY RECOMMEND SETTING
    # UP YOUR OWN RSS-FEED WITH SHOWRSS: http://www.showrss.info
    inputs:
      - rss: http://showrss.info/[YOUR-RSS-FEED-SPECIAL-LIST](/YOUR-RSS-FEED-SPECIAL-LIST)
    verify_ssl_certificates: no
    # WHERE TO PUT THE TORRENTS FOR TRANSMISSION TO FIND
    download: /c/transmission/watch-dir/
    # WE DON'T WANT EXISTING EPISODES TO BE DOWNLOADED
    # EMIT YOUR SERIES-DIR/S BELOW 
    exists_series: /media/Series/
    # ADD/REMOVE SERIES BELOW TO FIT YOUR NEEDS
    series:
      - [SERIES-1](/SERIES-1)
      - [SERIES-2](/SERIES-2)
      - [SERIES-3](/SERIES-3)
      - [SERIES-4](/SERIES-4)
    # WHAT QUALITY WILL BE DOWNLOADED? 720p, 1080p
    # COULD REPLACE THE BELOW HDTV.
    quality: hdtv

  movie:
    verify_ssl_certificates: no
    # WHERE TO PUT THE TORRENTS FOR TRANSMISSION TO FIND
    download: /c/transmission/watch-dir/
    # WE DON'T WANT EXISTING MOVIES TO BE DOWNLOADED
    # EMIT YOUR MOVIE-DIR/S BELOW
    exists_movie:
      - /media/Videos/
      - /USB/USB_HDD_1/Videos/
    # WHAT QUALITY WILL BE DOWNLOADED? YOU CAN
    # REPLACE THE BELOW STATED WITH HDTV.
    quality:
      - 1080p
      - 720p
    movie_queue: accept

  movie-queue-request:
    # WE WANT EVERYTHING IN OUR WATCHLIST TO BE ACCEPTED
    # TO OUR QUEUE. NOTHING IS DOWNLOADED YET.
    accept_all: yes
    # WE ONLY WANT MOVIES SEEN TO BE REJECTED WITH
    # THIS TASK. TV-TEMPLATE WILL NOT AFFECT THIS.
    seen: local
    retry_failed:
      max_retries: 10
    # NOW ADD ALL ENTRIES TO OUR QUEUE
    movie_queue: add
    # USER_ID AND WATCHLIST TO USE. ONLY PUBLIC LISTS
    # WILL WORK WITH THIS.
    imdb_list:
      list: watchlist
      user_id: urXXXXXXXX

  movie_search_request:
    template: movie
    torrent_alive: yes
    discover:
      what:
        - emit_movie_queue: yes
      # WHERE TO SEARCH FOR MOVIES. I USE HIGHRES MOVIES
      # AND QUALITY IS SET IN MOVIE-TEMPLATE. KAT-PLUGIN
      # IS MODYFIED TO WORK WITH NEW KICKASS.TO ADDRESS
      # WITH IS https://kat.cr. CHANGE FILE search_kat.py
      # RSS-FEED IS ONLY HERE TO SHOW IT CAN BE USED.
      from:
        - search_rss: http://your-movies-rss.com
        - kat:
            category: movies

#####################################################################################
#
# We now want to start downloading all we have set up. Lets start by calling the
# queue and fill it with entries. This have to be run before the search so it has
# highest priority. After the queue is filled with movies from IMDB-watchlist all
# entries is searched for with the assigned plugins.
# Lastly we run our tv-show task to get newest episodes :)
#
#####################################################################################

tasks:
  movie_queue:
    priority: 1
    template: movie-queue-request
    disable: retry_failed

  movie_search:
    priority: 2
    template: movie_search_request

  TVshows:
    template: tv
```

### Attachments
* [html-downloaded.template](/attachments/Cookbook/Users/KnockiMov/html-downloaded.template)
* [config.yml.knockimov](/attachments/Cookbook/Users/KnockiMov/config.yml.knockimov)