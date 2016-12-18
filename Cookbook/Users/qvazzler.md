**Note:** If you are using the season pack config along with any regular config, it is important that you run the trakt scrobbler either via Plex or Kodi to update your collection. Without the scrobbler you'll see some wonky behaviour since the season pack downloader will bump up your owned episodes in series, causing the regular config to expect to download an episode you actually already have thanks to the other config.

## Intro
Many private trackers have a rule that when a season is finished, all episodes are removed from it, and a season pack is created, often in a separate category like "Archive".
This config effectively downloads all season packs of a show you are following.

**Pros:**

+ Makes you able to watch a new show that already has a few seasons out, _without_ manually downloading the first couple of seasons.

+ Uses trakt.tv where you can add things you want to watch to your watchlist with ONE click. No more setting up RSS feeds and so on.

**Cons:**

-- Will always download season packs even if your other config has already downloaded all of the episodes in that season. (On the upside, most season packs are freeleech, so no real harm except bandwidth)

-- The contents of this config cannot be put into your main config, because it will screw up your database. use start parameter **-c seasonpack.config.yml** so it is 100% sure to use its own db.

-- Config is part of a larger solution. You will have to adjust things to suit your solution. (ex: Scrobbler needed for Season pack config)

-- Season pack config probably will not work if you are searching in a category that contains both Season packs and regular episodes. You'll have to play with the content filter or something like that.

## How does it work?

The config retrieves whatever TV Show is on your watchlist, and searches on torrent sites for <Name> <Season Number>. Example: Arrow 01

As the titles are being manipulated from trakt.tv to remove all episode information, it becomes a "hack" for how to download season packs instead. (from Arrow S02E01 to Arrow 02)

## The Season Packs Config using Trakt.tv
```
secrets: secrets.yml

# Things that need to be executed as command to new config db
# * flexget -c config.yml trakt auth <account_name>

# run with for example this command : "flexget -c config.yml -l logs/flexget.log -L debug daemon start --daemonize"

schedules:
  - tasks: [get_series_packs](/get_series_packs)
    interval:
      hours: 1

templates:
  global:
    torrent_alive: yes #number of seeders needed to accept
    domain_delay:
      sceneaccess.eu: 30 seconds
      sceneaccess.org: 30 seconds
  transmit-series:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '{{ secrets.transmission.download_path }}'
tasks:
  get_series_packs:
    priority: 2
    content_size:
      min: 1000
    regexp:
      reject:
        - \.[sS](/sS)\d\d[eE](/eE)\d\d\.
    configure_series:
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: 2-b-shows-b-get-backlog
          type: shows
          strip_dates: yes
      settings:
        timeframe: 2 hours
        target: 720p hdtv
        identified_by: sequence
        sequence_regexp: \b[S](/S)[0](/0)?(\d+)\b
        exact: yes
    manipulate:
      - title:
          replace:
            regexp: '(?<=\.[Ss](/Ss)\d\d)[eE](/eE)01(?=\.)' # Remove E01 from each episode and turn it into a "Season entry"
            format: ''
      - title:
          replace:
            regexp: '.*([eE](/eE)0[^1](/^1)).*|.*[eE](/eE)([1-9](/1-9)\d).*' # Remove any entry that is not the first episode of a season
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
    template:
      - transmit-series
```

Notes about the packs config:
- It is important that you are using a private tracker with good torrent structure. Using a public tracker like piratebay is _most likely_ going to cause problems.
- You'll need to create a secrets.yml file alongside this config.
  
  
  

## If you want a decent episode and movie downloading config to go alongside this, please use the below which features:
- Runs as a daemon. Execute it with 
```
flexget -c config.yml -l logs/flexget.log -L verbose daemon start --daemonize
```

- Retrieving movies/shows from the trakt watchlist and putting them in a seperate list so they won't disappear (meaning you only ever have to add shows to the watchlist when adding shows, convenience)
- Figures out which episode to download next thanks to scrobbling, aka no need to look into the filesystem where your media is
- Downloading shows/movies
- Clean up ended and downloaded shows from the lists so flexget doesn't have to keep searching for them
- Has an untested file delete task for shows/movies you haven't literally touched in a long time

## General Purpose Config using Trakt.tv
```
secrets: secrets.yml

#run with 'flexget -c config.yml -l logs/flexget.log -L verbose daemon start --daemonize'
#set webui password with 'flexget -c config.yml web passwd <some_password>'
#set trakt access with 'flexget -c config.yml trakt auth <your_account_name>'

#web_server:
#  bind: 0.0.0.0
#  port: 3540
#api: yes
#webui: yes

schedules:
  - tasks: [copy_trakt_watchlist, copy_trakt_watchlist_movies, fill_movie_list, get_movies_720p, get_series_begin, get_series]
    interval:
      hours: 2
  - tasks: [clean_trakt_movies_list, clean_trakt_shows_list, clean_trakt_shows_backlog_list]
    interval:
      days: 5

templates:
  global:
    retry_failed:
      retry_time: 5 minutes # Base time in between retries
      retry_time_multiplier: 1 # Amount retry time will be multiplied by after each successive failure
      max_retries: 25 # Number of times the entry will be retried
  get_series_standards:
    torrent_alive: yes #number of seeders needed to accept
    domain_delay:
      sceneaccess.eu: 30 seconds
      sceneaccess.org: 30 seconds
    content_size:
      max: 5000
      min: 60
  transmit-movies:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '{{ secrets.transmission.download_path_movies }}'
  transmit-series:
    transmission:
      host: '{{ secrets.transmission.host }}'
      port: 9091
      username: '{{ secrets.transmission.username }}'
      password: '{{ secrets.transmission.password }}'
      path: '{{ secrets.transmission.download_path_shows }}'
  download-movie:
    discover:
      what:
        - movie_list: 'movies from trakt'
      from:
        #- torrentleech:
            #rss_key: '{{ secrets.torrentleech.rss_key }}'
            #username: '{{ secrets.torrentleech.username }}'
            #password: '{{ secrets.torrentleech.password }}'
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 100
            category:
              browse:
                - Movies/x264
              archive:
                - Movies/Packs

      #ignore_estimations: no
    set:
      content_filename: "{{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }}) - {{ quality }}"
    template:
      - transmit-movies
  download-show:
    discover:
      what:
        - emit_series: yes
            #from_start: yes backfill: no
      from:
        #- torrentleech:
            #rss_key: '{{ secrets.torrentleech.rss_key }}'
            #username: '{{ secrets.torrentleech.username }}'
            #password: '{{ secrets.torrentleech.password }}'
        - sceneaccess:
            username: '{{ secrets.sceneaccess.username }}'
            password: '{{ secrets.sceneaccess.password }}'
            gravity_multiplier: 100
            category:
              browse:
                - TV/HD-x264
      release_estimations: strict #only download those with air dates
    set:
      content_filename: "{{ series_name }} - {{ series_id }} ({{ quality|upper }})"
    template:
      - transmit-series
tasks:
  copy_trakt_watchlist:
    priority: 1
    disable: seen
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: watchlist
      type: shows
    accept_all: yes
    list_add:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.shows_follow }}'
  copy_trakt_watchlist_movies:
    priority: 2
    disable: seen

    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: watchlist
      type: movies
    accept_all: yes
    if:
      - trakt_collected: reject
    list_add:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.movies_get }}'
  fill_movie_list:
    priority: 3
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: '{{ secrets.trakt_lists.movies_get }}'
      type: movies
    accept_all: yes
    list_add:
      - movie_list: 'movies from trakt'
  get_movies_720p:
    torrent_alive: yes #number of seeders needed to accept
    priority: 4
    content_size:
      max: 23040
      min: 1024
    quality: 720p bluray+
    template: download-movie
  get_series_begin:
    priority: 5
    disable: seen
    trakt_emit:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: '{{ secrets.trakt_lists.shows_follow }}'
      context: collected
      position: next
    accept_all: yes
    set_series_begin: yes
  get_series:
    priority: 6
    configure_series:
      settings:
        #quality: 720p hdtv+
        timeframe: 6 hours
        target: 720p hdtv
        identified_by: ep
        exact: yes
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.shows_follow }}'
          type: shows
    template:
      - get_series_standards
      - download-show

  get_series_direct:
    manual: yes
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    configure_series:
      settings:
        quality: 720p hdtv+
        exact: yes
      from:
        trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.shows_follow }}'
          type: shows
    template: transmit-series

  get_movies_direct:
    manual: yes
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    content_size:
      max: 23040
      min: 1024
    quality: 720p bluray+
    list_queue:
      - movie_list: 'movies from trakt'
    template: transmit-movies

  # MANUAL TASKS BELOW

  clean_trakt_movies_list:
    priority: 8
    disable:
      - seen
      - movie_queue
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: '{{ secrets.trakt_lists.movies_get }}'
      type: movies
      strip_dates: yes
    if:
      - trakt_collected: accept
    list_remove:
      - movie_list: 'movies from trakt'
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.movies_get }}'

  clean_trakt_shows_list:
    priority: 9
    disable: seen
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: '{{ secrets.trakt_lists.shows_follow }}'
      type: shows
      strip_dates: yes
    if:
      - trakt_collected and (trakt_series_status == 'ended' or trakt_series_status == 'cancelled'): accept
    list_remove:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.shows_follow }}'

  clean_trakt_shows_backlog_list:
    priority: 10
    disable: seen
    trakt_lookup:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
    trakt_list:
      username: '{{ secrets.trakt.username }}'
      account: '{{ secrets.trakt.account }}'
      list: '{{ secrets.trakt_lists.shows_backlog }}'
      type: shows
      strip_dates: yes
    if:
      - trakt_collected and (trakt_series_status == 'ended' or trakt_series_status == 'cancelled'): accept
    list_remove:
      - trakt_list:
          username: '{{ secrets.trakt.username }}'
          account: '{{ secrets.trakt.account }}'
          list: '{{ secrets.trakt_lists.shows_backlog }}'

  old_files:
    manual: yes
    disable:
      #- builtins
      - backlog
      - seen
      - retry_failed
    limit_new: 1     
    filesystem:
      path:
        - /home/qvazzler/testdir/
      retrieve:
        #- files
        - dirs
      #regexp: '.+\..+'

    age:
      field: 'accessed'
      age: '1 second'
      action: 'accept'

    set:
      series_name: "{{'title'}}"

    trakt_lookup:
      account: '{{ secrets.trakt.account }}'
      username: '{{ secrets.trakt.username }}'

    if:
      - trakt_watched == False: reject

    #exec:    
      #on_exit:
        #for_accepted: rm -r '{{location}}'
```

Notes about the general purpose config:
- I left the Web UI disabled. It can be re-enabled, but you then need to set a password (see [https://flexget.com/wiki/Web-UI](/https://flexget.com/wiki/Web-UI))
- The General purpose config will clean up entries from your lists that have been watched already.
- The old_files task is UNTESTED! Use with caution.

Notes about both of my configs:
- I don't need to worry about where to put my files as I have a bash script that executes Filebot on the files. You might need to modify based on your own needs here.
- You will most likely not be able to copy this config directly. Please make edits where suitable for you.