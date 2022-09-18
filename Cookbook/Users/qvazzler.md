---
title: qvazzler
description: 
published: true
date: 2022-09-18T05:23:30.693Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:27.917Z
---


**Note:** Season pack support is now officially supported by FlexGet without any ugly hacks like I've previously shown below. I am now extending my configuration to include irc daemon usage, but season pack support is still in there.

# Multi-config/user solution using the IRC daemon

> This guide is very complex (+ work in progress) and has many smaller use-cases baked into a big guide. You will find gaps in documentation throughout the writing and sometimes a LOT of commented lines, but I expect experienced FlexGet users to pick it up from there. I am available if you @mention me from Gitter. If you are new to FlexGet you may have a hard time.
{.is-error}

## Intro
One issue that many flexget users have suffered in the past has been the lack of speed to get to those latest torrents. That is, until users cvium and liight gave us the IRC daemon, which acts similarly to autodl.

Now if you are like me, you are managing multiple configurations, maybe on behalf of friends or family. This should hopefully set you along the right path.

I am assuming that you have decent skill in the linux shell (bash/others).

**Pros:**

+ Ability to use a single IRC daemon for multiple user configs on the same machine.
+ Season pack support
+ Trakt support
+ Various cleaner tasks

**Cons:**

* Takes a little longer to get right.

## How does it work?

Basically you have one IRC Daemon config, along with other regular configs.

Whenever a new torrent is announced in an IRC channel you're in, the irc daemon sends that torrent to the api of each of the regular user configs.

## The IRC Config
```
variables: variables.yml
schedules: no

templates:
  global:
    disable: seen
    accept_all: yes    

irc:
  torrentleech:
    tracker_file: '{? general.config_path ?}/{? torrentleech.trackerfile ?}'
    nickname: '{? torrentleech.qvazzler.nickname ?}'
    nickserv_password: '{? torrentleech.qvazzler.nickserv_password ?}'
    port: 7011
    rsskey: '{? torrentleech.qvazzler.rsskey ?}'
    channels: ["#tlannounces"]
    task_re:
      torrentleech:
        - regexp: '(TV :: Episodes HD)|(Movies :: Bluray)|(Movies :: WEBRip)|(Movies :: BDRip)'
          field: irc_category
  iptorrents:
    tracker_file: '{? general.config_path ?}/{? iptorrents.trackerfile ?}'
    nickname: '{? iptorrents.qvazzler.nickname ?}'
    nickserv_password: '{? iptorrents.qvazzler.nickserv_password ?}'
    port: 6667
    passkey: '{? iptorrents.qvazzler.passkey ?}'
    channels: ["#ipt.announce"]
    task_re:
      iptorrents:
        - regexp: (TV\/x265)|(TV\/x264)|(TV\/Web-DL)|(Movie\/Web-DL)|(Movie\/HD\/Bluray)
          field: irc_category
  morethantv:
    tracker_file: '{? general.config_path ?}/{? morethantv.qvazzler.trackerfile ?}'
    nickname: '{? morethantv.qvazzler.nickname ?}'
    nickserv_password: '{? morethantv.qvazzler.nickserv_password ?}'
    torrent_pass: '{? morethantv.qvazzler.torrent_pass ?}'
    port: 6667
    task: morethantv
    authkey: '{? morethantv.qvazzler.authkey ?}'
    channels: ["#Announce"]
  #sceneaccess:
    #tracker_file: '{? general.config_path ?}/{? sceneaccess.trackerfile ?}'
    #port: 6667
    #nickname: '{? sceneaccess.moldrag.nickname ?}'
    #nickserv_password: '{? sceneaccess.moldrag.nickserv_password ?}'
    #authkey: '{? sceneaccess.moldrag.authkey ?}'
    #channels: ["#announce"]
    #task_re:
      #sceneaccess:
        #- regexp: (Movies\/DVD-R)|(Movies\/x264)|(TV\/HD-x264)|(TV\/SD-x264)
          #field: irc_category
  alpharatio:
    tracker_file: '{? general.config_path ?}/{? alpharatio.trackerfile ?}'
    port: 6667
    nickname: '{? alpharatio.qvazzler.nickname ?}'
    invite_nickname: voyager
    invite_message: 'enter {? alpharatio.qvazzler.irc_key ?}'
    torrent_pass: '{? alpharatio.qvazzler.torrent_pass ?}'
    authkey: '{? alpharatio.qvazzler.authkey ?}'
    task_re:
      alpharatio:
        - regexp: (MovieHD)|(TvHD)|(TvDVDRip)
          field: category

tasks:
  sceneaccess:
    exec:
      on_output:
        for_accepted: 
          - >- 
            bash
            '{? general.config_path?}/{? general.notifyscript ?}'
            "{?title?}"
            "{?url?}"
            "{?subscribers.moldrag.url?}"
            >> "{? general.config_path ?}/logs/injections/{?task?}/{?title?}.log"
          #- >-
            #bash
            #'{? general.config_path?}/{? general.notifyscript ?}'
            #"{?title?}"
            #"{?url|replace(sceneaccess.moldrag.authkey, sceneaccess.qvazzler.authkey)?}"
            #"{?subscribers.qvazzler.url?}"
            #>> "{? general.config_path ?}/logs/{?task?}/{?title?}.log"

  torrentleech:
    exec:
      on_output:
        for_accepted: 
          - >-
            bash
            '{? general.config_path?}/{? general.notifyscript ?}'
            "{?title?}"
            "{?url?}"
            "{?subscribers.qvazzler.url?}"
            >> "{? general.config_path ?}/logs/{?task?}/{?title?}.log"
          - >-
            bash
            '{? general.config_path?}/{? general.notifyscript ?}'
            "{?title?}"
            "{?url|replace(torrentleech.qvazzler.rsskey, torrentleech.Lorien.rsskey)?}"
            "{?subscribers.ringwall.url?}"
            >> "{? general.config_path ?}/logs/{?task?}/{?title?}.log"
  iptorrents:
    exec:
      on_output:
        for_accepted: >-
          bash
          '{? general.config_path?}/{? general.notifyscript ?}'
          "{?title?}"
          "{?url?}"
          "{?subscribers.qvazzler.url?}"
          >> "{? general.config_path ?}/logs/{?task?}/{?title?}.log"
  morethantv:
    exec:
      on_output:
        for_accepted: >-
          bash
          '{? general.config_path?}/{? general.notifyscript ?}'
          "{?title?}"
          "{?url?}"
          "{?subscribers.qvazzler.url?}"
          >> "{? general.config_path ?}/logs/{?task?}/{?title?}.log"
```

This config is accompanied by a `trackers` directory, that contains XML information about each of the trackers available through IRC. [Read about the IRC Daemon to find out more.](Plugins/Daemon/irc).

## The variables.yml file

Just so you get the idea, it looks like this.

```
general:
  config_path: '/home/flexget/.virtualenvs/irc_daemon'
  notifyscript: 'notify_daemons.sh'

subscribers:
  qvazzler:
    url: 'http://api.myflexgetmachine.com:3540'
  user2:
    url: 'http://anotherhost:3541'
  anotheruser:
    url: 'http://127.0.0.1:3542'
  fourthuser:
    url: 'http://localhost:3543'

alpharatio:
  trackerfile: 'trackers/AlphaRatio.tracker'
  qvazzler:
    irc_key: x
    authkey: x
    torrent_pass: x
    nickname: qvazzler-bot
  moldrag:
    irc_key: x
    authkey: x
    torrent_pass: x
    nickname: moldrag-bot

sceneaccess:
  trackerfile: 'trackers/SceneAccess.tracker'
  qvazzler:
    authkey: x
    nickname: qvazzler-bot
    nickserv_password: x
  moldrag:
    authkey: x
    nickname: moldrag-bot

```

It can feel a bit daunting figuring out all the variables by yourself. The best way to get a good idea is to look inside the trackers file that you've gotten from the autodl community, what variables they surface in it. Also the reading the IRC rules in whatever place you're getting the trackers from is a good idea. (For example, appending -bot to your nick is required in many rules when you downloading stuff automatically)

## This irc daemon instance uses bash scripts to notify the flexget API's

Below is a decent example of how that script would look like.

You can read more about the [FlexGet API on the wiki.](API).
If you want to get the flexget token for one of your regular flexget instances, make sure API is enabled in your config (`web_server: yes`), password has been generated (`flexget web passwd <some_password>`) and after, use command `flexget web showtoken`.

```
#!/bin/bash

TITLE=$1
URL=$2

declare -A daemons

# How the command is being executed from irc daemon
#./notify_daemons.sh "MovieName 2016 BDRip 720p X265 ReleaseGroupName" "https://www.iptorrents.com/download.php/123/file.torrent" "http://192.168.1.100:3540"

#the tokens below are faked. Put in the real ones yourself (and the correct ip/port of course)
#daemons["http://192.168.1.100:3541"]="token_here" #user 1, inactive
daemons["http://192.168.1.100:3542"]="another_token...b915c3eb0b5800f424320e5cc82b03edc5a5b5850aczzzzzzzzzzzzc" #user 2
daemons["http://192.168.1.100:3543"]="another...fwaff67dbczczczwczwcwdwdwddwwdwdwqqqrrrrrrrde22696b376a1" #user 3

# If specific hostname was supplied, proceed to only notify that host
if [ $# -eq 3 ]; then
  for daemon in "${!daemons[@]}"; do
    echo "compare ${daemon} against $3"
    if [ ${daemon} != $3 ]; then
      unset daemons[${daemon}]
    fi
  done
fi

#Now run the actual query
for daemon in "${!daemons[@]}"; do
curl -H "Authorization: Token ${daemons[${daemon}]}" -m 300 -X POST --header "Content-Type: application/json" --header "Accept: application/json" -d "{\
\"disable_tracking\": true,\
\"discover_now\": false,\
\"entry_dump\": true,\
\"inject\": [\
{\
\"accept\": false,\
\"fields\": {},\
\"force\": false,\
\"title\": \"${TITLE}\",\
\"url\": \"${URL}\"\
}\
],\
\"learn\": false,\
\"loglevel\": \"debug\",\
\"no_cache\": true,\
\"now\": true,\
\"progress\": true,\
\"summary\": true,\
\"tasks\": [\
\"get_series_direct\",\
\"get_movies_direct\"\
]\
}" "${daemon}/api/inject/"
done
```

## Here's what one of the regular configs look like. (NOTE: Uses Trakt, you need a scrobbler via XBMC/Kodi or Plex)
- Runs as a daemon. Execute it with 
```
flexget -c config.yml -l logs/flexget.log -L verbose daemon start --daemonize
```

You'll note that there's a task suffixed "_direct" for movies and shows, which are used by the IRC daemon. There is also a task for season packs. There is a lot of commented stuff throughout the configs, I am leaving them in for you to take inspiration from.

```
variables: variables.yml
# Things that need to be updated here in case of config-copy (because they are integers..)
# * 'port' fields (note: web_server port needs to be different from other instances!)
# * iptorrents 'uid' field

# Things that need to be executed as command to new config db
# * flexget -c config.yml web passwd <new_password>
# * flexget -c config.yml trakt auth <account_name>

web_server:
  bind: 0.0.0.0
  port: 3540
  web_ui: yes

schedules:
  - tasks: [copy_trakt_follow_watchlist, copy_trakt_backlog_watchlist, copy_trakt_watchlist_movies, fill_movie_list, get_movies_720p, get_series_begin, get_series, get_series_packs]
    interval:
      hours: 1
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
  transmit-movies:
    transmission:
      host: '{? transmission.host ?}'
      port: 80
      username: '{? transmission.username ?}'
      password: '{? transmission.password ?}'
      path: '{? transmission.download_path_movies ?}'
  transmit-series:
    transmission:
      host: '{? transmission.host ?}'
      port: 80
      username: '{? transmission.username ?}'
      password: '{? transmission.password ?}'
      path: '{? transmission.download_path_shows ?}'
  download-movie:
    discover:
      what:
        - movie_list: 'movies from trakt'
      from:
        - morethantv:
            username: '{? mtv.username ?}'
            password: '{? mtv.password ?}'
            category:
              - Movies
            #tags: [adventure]
            all_tags: yes
        #- torrentleech:
            #rss_key: '{? torrentleech.rss_key ?}'
            #username: '{? torrentleech.username ?}'
            #password: '{? torrentleech.password ?}'
        #- iptorrents:
            #rss_key: '{? iptorrents.rss_key ?}'
            #uid: 123
            #password: '{? iptorrents.password ?}'
            #category:
              #- Movie-HD-Bluray
              #- Movie-DVD-R
        # This is only for season pack downloading
        #- sceneaccess:
            #username: '{? sceneaccess.username ?}'
            #password: '{? sceneaccess.password ?}'
            #gravity_multiplier: 100
            #category:
              #browse:
                #- Movies/x264
              #archive:
                #- Movies/Packs

      #ignore_estimations: no
    #set:
      #content_filename: "{? imdb_name|replace('/', '_')|replace(':', ' -') ?} ({? imdb_year ?}) - {? quality ?}"
    template:
      - transmit-movies
  download-show:
    discover:
      what:
        - next_series_episodes: yes
            #backfill: yes
            #from_start: yes
      from:
        - morethantv:
            username: '{? mtv.username ?}'
            password: '{? mtv.password ?}'
            category:
              - TV
            #tags: [adventure]
            all_tags: yes
        #- torrentleech:
            #rss_key: '{? torrentleech.rss_key ?}'
            #username: '{? torrentleech.username ?}'
            #password: '{? torrentleech.password ?}'
        #- iptorrents:
            #rss_key: '{? iptorrents.rss_key ?}'
            #uid: 123
            #password: '{? iptorrents.password ?}'
            #category:
              #- TV-x264
              #- TV-Web-DL
        #- sceneaccess:
            #username: '{? sceneaccess.username ?}'
            #password: '{? sceneaccess.password ?}'
            #gravity_multiplier: 100
            #category:
              #archive:
                #- TV/HD-x264

      release_estimations: strict #only download those with air dates
    #set:
      #content_filename: "{? series_name ?} - {? series_id ?} ({? quality|upper ?})"
    template:
      - transmit-series
  download-show-pack:
    discover:
      what:
        - next_series_seasons: yes
            #backfill: yes
            #from_start: yes
      from:
        - sceneaccess:
            username: '{? sceneaccess.username ?}'
            password: '{? sceneaccess.password ?}'
            gravity_multiplier: 100
            category:
              archive:
                - TV/Packs

      release_estimations: strict #only download those with air dates
    #set:
      #content_filename: "{? series_name ?} - {? series_id ?} ({? quality|upper ?})"
    template:
      - transmit-series
tasks:
  copy_trakt_follow_watchlist:
    priority: 1
    disable: seen
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.shows_follow ?}'
      type: shows
    accept_all: yes
    list_add:
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: watchlist
  copy_trakt_backlog_watchlist:
    priority: 2
    disable: seen
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.shows_backlog ?}'
      type: shows
    accept_all: yes
    list_add:
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: watchlist
  copy_trakt_watchlist_movies:
    priority: 3
    disable: seen
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.movies_get ?}'
      type: movies
    accept_all: yes
    list_add:
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: watchlist
  fill_movie_list:
    priority: 4
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.movies_get ?}'
      type: movies
    accept_all: yes
    list_add:
      - movie_list: 'movies from trakt'
  get_movies_720p:
    torrent_alive: yes #number of seeders needed to accept
    priority: 5
    list_match:
      from:
        - movie_list: 'movies from trakt'
    content_size:
      max: 23040
      min: 1024
    quality: 720p bluray+
    template: download-movie

  get_series_begin:
    priority: 6
    disable: seen
    next_trakt_episodes:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: 'watchlist'
      context: collected
      position: next
    accept_all: yes
    set_series_begin: yes

  get_series:
    priority: 7
    configure_series:
      settings:
        timeframe: 6 hours
        season_packs: no
        target: 720p hdtv
        identified_by: ep
        exact: yes
      from:
        trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.shows_follow ?}'
          type: shows
    template:
      - get_series_standards
      - download-show

  get_series_packs:
    priority: 8
    configure_series:
      settings:
        timeframe: 6 hours
        season_packs: only
        target: 720p hdtv
        identified_by: ep
        exact: yes
      from:
        trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.shows_backlog ?}'
          type: shows
    template:
      - get_series_standards
      - download-show-pack

  get_series_direct:
    manual: yes
    trakt_lookup:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
    configure_series:
      settings:
        quality: 720p hdtv+
        exact: yes
      from:
        trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.shows_follow ?}'
          type: shows
    template: transmit-series

  get_movies_direct:
    manual: yes
    trakt_lookup:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
    content_size:
      max: 23040
      min: 1024
    quality: 720p bluray+
    list_match:
      from:
        - movie_list: 'movies from trakt'
    template: transmit-movies
  # MANUAL TASKS BELOW

  clean_trakt_movies_list:
    priority: 9
    disable:
      - seen
      - movie_queue
    trakt_lookup:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.movies_get ?}'
      type: movies
      strip_dates: yes
    if:
      - trakt_collected: accept
    list_remove:
      - movie_list: 'movies from trakt'
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.movies_get ?}'

  clean_trakt_shows_list:
    priority: 10
    disable: seen
    trakt_lookup:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.shows_follow ?}'
      type: shows
      strip_dates: yes
    if:
      - trakt_collected and (trakt_series_status == 'ended' or trakt_series_status == 'cancelled'): accept
    list_remove:
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.shows_follow ?}'

  clean_trakt_shows_backlog_list:
    priority: 11
    disable: seen
    trakt_lookup:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
    trakt_list:
      username: '{? trakt.username ?}'
      account: '{? trakt.account ?}'
      list: '{? trakt_lists.shows_backlog ?}'
      type: shows
      strip_dates: yes
    if:
      - trakt_collected: accept
    list_remove:
      - trakt_list:
          username: '{? trakt.username ?}'
          account: '{? trakt.account ?}'
          list: '{? trakt_lists.shows_backlog ?}'

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
        - /tmp/
      retrieve:
        #- files
        - dirs
      #regexp: '.+\..+'

    age:
      field: 'accessed'
      age: '1 second'
      action: 'accept'

    set:
      series_name: "{?'title'?}"

    trakt_lookup:
      account: '{? trakt.account ?}'
      username: '{? trakt.username ?}'

    if:
      - trakt_watched == False: reject

    #exec:    
      #on_exit:
        #for_accepted: rm -r '{?location?}'
```

A small snippet of variables.yml (you get the idea):

```
trakt_lists:
  shows_follow: 1-b-shows-b-follow
  shows_backlog: 2-b-shows-b-get-backlog
  movies_get: 3-b-movie-b-get
```

These are the names of the lists I use in trakt. You will need to create your own lists and provide their URL names here. I have 1-b etc because I've sneaked in some html into my list names, and that gives you 1-b-.. etc in the URL.

Notes about the user config:
- The old_files task is UNTESTED! Use with caution.
