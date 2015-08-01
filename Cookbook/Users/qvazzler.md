'''Note:''' This config is currently outdated, and therefore slightly borked. Feel free to take inspiration from it, but it won't work 100% after copy-paste.

== Intro ==

Many private trackers have a rule that when a season is finished, all episodes are removed from it, and a season pack is created, often in a separate category like "Archive".

This config effectively downloads all season packs of a show you are following.

'''Pros:'''

+ Makes you able to watch a new show that already has a few seasons out, _without_ manually downloading the first couple of seasons.

+ Uses trakt.tv where you can add things you want to watch to your watchlist with ONE click. No more setting up RSS feeds and so on.

'''Cons:'''

-- Will always download season packs even if your other config has already downloaded all of the episodes in that season. (On the upside, most season packs are freeleech, so no real harm except bandwidth)

-- The contents of this config cannot be put into your main config, because it will screw up your database. use start parameter '''-c this.config.yml''' so it is 100% sure to use its own db.

-- Config is part of a larger solution. You will have to adjust things to suit your solution.

== How does it work? == 

The config retrieves whatever TV Show is on your watchlist, and searches on torrent sites for <Name> <Season Number>. Example: Arrow 01

As the titles are being manipulated from trakt.tv to remove all episode information, it becomes a "hack" for how to download season packs instead. (from Arrow S02E01 to Arrow 02)

== The Season Packs Config using Trakt.tv ==
{{{
#Make sure to run as --discover-now --no-cache
secrets: secrets.yml
templates:
  global:
    torrent_alive: yes #number of seeders needed to accept
    retry_failed:
      retry_time: 5 minutes # Base time in between retries
      retry_time_multiplier: 1 # Amount retry time will be multiplied by after each successive failure
      max_retries: 15 # Number of times the entry will be retried
  transmit-series:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '/volume1/Disk1/Library/Transmission/Uncategorized/TV Shows/'

tasks:
  get_series_packs:
    priority: 2
    content_size:
      min: 3072
    regexp:
      reject:
        - \.[sS]\d\d[eE]\d\d\.
        - \.FiX\.
        - FASTSUB #French
        - VOSTFR #French
        - Subtitulado #Spanish
        - Special-Wicked #Special trailer episodes from Once Upon a Time
        - Magazine #No magazines on Arrow, thank you.
        - NLsubs
    content_filter:
      reject:
        - '*.avi' #Uhgg Jak!
    verify_ssl_certificates: no
    configure_series:
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          password: '{{ secrets.trakt.password }}'
          list: watchlist
          type: shows
          strip_dates: yes
      settings:
        quality: 480p-720p <=hdtv
        identified_by: sequence
        sequence_regexp: \b[S][0]?(\d+)\b
        exact: yes
    manipulate:
      - title:
          replace:
            regexp: '(?<=\.[Ss]\d\d)[eE]01(?=\.)' # Remove E01 from each episode and turn it into a "Season entry"
            format: ''
      - title:
          replace:
            regexp: '.*([eE]0[^1]).*|.*[eE]([1-9]\d).*' # Remove any entry that is not the first episode of a season
            format: ''
    discover:
      what:
        - emit_series:
            from_start: yes
            backfill: yes
      from:
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 200
            category:
              archive:
                - TV/Packs
    template: transmit-series
}}}

Notices about the packs config:
- It is important that you are using a private tracker with good torrent structure. Using a public tracker like piratebay is _most likely_ going to cause problems.
- You'll need to create a secrets.yml file alongside this config.

If you want a decent episode and movie downloading config to go alongside this, please use the below:

== General Purpose Config using Trakt.tv ==
{{{
#Make sure to run as --discover-now --no-cache
secrets: secrets.yml
templates:
  global:
    torrent_alive: yes #number of seeders needed to accept
    retry_failed:
      retry_time: 5 minutes # Base time in between retries
      retry_time_multiplier: 1 # Amount retry time will be multiplied by after each successive failure
      max_retries: 15 # Number of times the entry will be retried
  transmit-movies:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '/volume1/Disk1/Library/Transmission/Uncategorized/Movies/'
  transmit-series:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '/volume1/Disk1/Library/Transmission/Uncategorized/TV Shows/'
  download-movie:
    verify_ssl_certificates: no
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 200
            category:
              browse:
                - Movies/x264
              archive:
                - Movies/Packs
    movie_queue: accept
    set:
      content_filename: "{{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }}) - {{ quality }}"
    template: transmit-movies

tasks:
  fill_movie_queue:
    priority: 1
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      password: '{{ secrets.trakt.password }}'
      list: watchlist
      #strip_dates: yes
      type: movies
    accept_all: yes
    movie_queue: add

  #Last resort if movie can't be found
  get_movies_720p:
    priority: 2
    content_size:
      max: 15360
      min: 1024
    exists_movie:
      - /volume1/Disk1/Library/Movies
    #assume_quality: 720p bluray #in case of REALLY long titles
    quality: 480p-720p bluray+
    movie_queue: accept
    template: download-movie

  get_series:
    priority: 3
    content_size:
      max: 3072
      min: 60
    exists_series:
      - /volume1/Disk1/Library/TV Shows/
    regexp:
      reject:
        - FASTSUB #French
        - VOSTFR #French
        - Subtitulado #Spanish
        - Special-Wicked #Special trailer episodes from Once Upon a Time
        - Magazine #No magazines on Arrow, thank you.
        - NLsubs
    content_filter:
      reject:
        - '*.avi' #Uhgg Jak!
    verify_ssl_certificates: no
    discover:
      what:
        - emit_series:
            from_start: yes
            backfill: yes
      from:
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 200
            category:
              browse:
                - TV/HD-x264
    configure_series:
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          password: '{{ secrets.trakt.password }}'
          list: watchlist
          type: shows
        listdir:
          - /volume1/Disk1/Library/TV Shows
      settings:
        quality: 480p-720p <=hdtv
        identified_by: ep
        exact: yes
    set:
      content_filename: "{{ series_name }} - {{ series_id }} ({{ quality|upper }})"
    template: transmit-series

  get_series_stripyear:
    priority: 4
    content_size:
      max: 3072
      min: 60
    exists_series:
      - /volume1/Disk1/Library/TV Shows/
    regexp:
      reject:
        - FASTSUB #French
        - VOSTFR #French
        - Subtitulado #Spanish
        - Special-Wicked #Special trailer episodes from Once Upon a Time
        - Magazine #No magazines on Arrow, thank you.
        - NLsubs
    content_filter:
      reject:
        - '*.avi' #Uhgg Jak!
    verify_ssl_certificates: no
    discover:
      what:
        - emit_series:
            from_start: yes
            backfill: yes
      from:
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 200
            category:
              browse:
                - TV/HD-x264
    configure_series:
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          password: '{{ secrets.trakt.password }}'
          list: watchlist
          type: shows
          strip_dates: yes
        listdir:
          - /volume1/Disk1/Library/TV Shows
      settings:
        quality: 480p-720p <=hdtv
        identified_by: ep
        exact: yes
    set:
      content_filename: "{{ series_name }} - {{ series_id }} ({{ quality|upper }})"
    template: transmit-series
}}}

Notices about both of my configs:
- I don't need to worry about where to put my files as I have a bash script that executes Filebot on the files.
- You will probably not be able to copy this config directly. Please make edits where suitable for you.

Finally, if you have any questions about this config, feel free to add me on steam (qvazzler), alternatively Skype (qvazzler)