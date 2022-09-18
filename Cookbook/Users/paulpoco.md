---
title: paulpoco
description: 
published: true
date: 2022-09-18T05:23:26.641Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:23:23.975Z
---

Example of my Config and Series files for Flexget 1.2.231

Using Next-Episode a source of TV series that can easily be added with Android app or their web site.
Automatically download movies based on IMDB ratings.
Automatically download torrents from a folder.

config.yml

```
templates:
  global:
    notifymyandroid:
      apikey: apikey_here
    # Make there's 50GB free before adding more downloads
    free_space:
      path: "/media/sdb2"
      space: 50000
    # Make sure all filenames are Windows safe (for samba)
    pathscrub: windows
    regexp:
      reject:
        - (s|d)ub(s|bed)?\b: {from: title}
        - \b(duo|tri|quadri|tetra|penta)logy\b: {from: title}
        - \b3-?D\b: {from: title}
        - \btrailer\b: {from: title}
        - \bR5\b: {from: title}
        - \bWEBSCR\b: {from: title}
        - \bscreener\b: {from: title}
        - \bTS\b: {from: title}
        - \bCam\b: {from: title}
        - '{C_P}': {from: title}
        - TrTd TeaM: {from: title}
        - \[TNTVillage\](/TNTVillage\): {from: title}
        - \[facepalm\](/facepalm\): {from: title}
        - \bASAP\b: {from: title}
    content_filter:
      reject:
        - 'password.txt' 
        - '*.rar'
        - '*.wmv'
        - '*.avi'
    domain_delay:
      bt-chat.com: 5 seconds
      torrentz.eu: 5 seconds
      thepiratebay.se: 10 seconds
  tv:
    configure_series:
      from:
        text:
          url: "http://next-episode.net/PAGES/misc/export_calendar?z&u=username&k=next-episode.ics"
          entry: 
            title: ^SUMMARY:(.*) - [0-9](/0-9)+x[0-9](/0-9)+.*$
            url: ^SUMMARY:(.*) - [0-9](/0-9)+x[0-9](/0-9)+.*$
    # a seperate yml to contain the shows next-episode.net doesn't have
    include: series.yml
    exists_series:
      - /media/sdb2/TV
      - /media/sdb2/Torrents
    thetvdb_lookup: yes
    set:
      quality: 720p hdtv+
      upgrade: yes
      path: "/media/sdb2/Torrents"
      movedone: "/media/sdb2/TV/{{ series_name }}/Season {{ series_season }}"
      content_filename: >
        {{ series_name }} - {{ series_id }}
        {% if tvdb_ep_name|default(False) %}- {{ tvdb_ep_name }} {% endif %}- {{ quality|upper }}
        {% if proper_count %}- proper{% if proper_count > 1 %}{{ proper_count }}{% endif %}{% endif %}
    deluge:
      username: xxxxxxxx
      password: xxxxxxxx
      queuetotop: yes
   
  moviesQue:
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - flexget_archive: yes
        - piratebay: yes
        #- newtorrents
    movie_queue: yes
    imdb:
      accept_languages:
        - english
      reject_mpaa_ratings:
        - X
    content_filter:
      reject: 
        - '*.rar'
        - '*.wmv'
        - '*.avi'
    content_size:
      max: 8000
      min: 675
    regexp:
      from: title
      reject:
        - ts
        - hindi
        - german
        - s\d+e\d+: {from: title}
        - '\d{4}.\d{2}.\d{2}': {from: title}
        - \d+x\d+: {from: title}        
    imdb_required: yes
    seen_movies: strict
    exists_movie: 
      - /media/sdb2/Movies
      - /media/sdb2/Torrents
    proper_movies: yes
    deluge:
      username: xbmc
      password: xbmcxbmc
      queuetotop: yes
    set:
      path: "/media/sdb2/Torrents"
      movedone: "/media/sdb2/Movies/{{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }})"
      content_filename: |
        {{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }}) - {{ quality }}
      label: movie
      addpaused: no
      ratio: 1

  movies:
    imdb:
      min_score: 7.0
      min_votes: 2000
      min_year: 2008
      reject_genres:
        - News
        - Documentary
        - Horror
        - Biography
        - Reality-Tv
        - Horror
        - Musical
        - Music
      accept_languages:
        - english
      reject_mpaa_ratings:
        - X
    content_filter:
      reject: 
        - '*.rar'
        - '*.wmv'
        - '*.avi'
    quality: dsr+ hdtv-bluray
    content_size:
      max: 8000
      min: 900
    regexp:
      from: title
      reject:
        - ts
        - hindi
        - german
        - s\d+e\d+: {from: title}
        - '\d{4}.\d{2}.\d{2}': {from: title}
        - \d+x\d+: {from: title}
    imdb_required: yes
    imdb_lookup: yes
    seen_movies: strict
    limit_new: 4
    exists_movie: 
      - /media/sdb2/Movies
      - /media/sdb2/Torrents
    proper_movies: yes
    deluge:
      username: xbmc
      password: xbmcxbmc
      queuetotop: yes
    set:
      path: "/media/sdb2/Torrents"
      movedone: "/media/sdb2/Movies/{{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }})"
      content_filename: |
        {{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }}) - {{ quality }}
      label: movie
      addpaused: no
      ratio: 1
    trakt_add:
      username: xxxxxxx
      password: xxxxxxx
      api_key: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      list: library
  movies2:
    imdb_lookup: yes
    exists_movie: 
      - /media/sdb2/Movies
      - /media/sdb2/Torrents
    deluge:
      username: xxxxxxxxxx
      password: xxxxxxxxxx
      queuetotop: yes
    set:
      path: "/media/sdb2/Torrents"
      movedone: "/media/sdb2/Movies/{{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }})"
      content_filename: |
        {{ imdb_name|replace('/', '_')|replace(':', ' -') }} ({{ imdb_year }}) - {{ quality }}
      label: movie
      addpaused: no
      ratio: 1
    trakt_add:
      username: xxxxxxxxx
      password: xxxxxxxxxx
      api_key: xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx
      list: library

tasks:
  karmorra:
    priority: 1
    template:
      - tv
    rss: http://showrss.info/feeds/all.rss

  bt_chat:
    priority: 1
    template:
      - tv
    rss: http://rss.bt-chat.com/?cat=9

  thepiratebay_tv:
    priority: 1
    template:
      - tv
    rss: http://rss.thepiratebay.se/208
 
  extratorrentTV:  
    priority: 1
    template:
      - tv
    rss: http://extratorrent.cc/rss.xml?cid=8&type=last

  torlock_tv:
    priority: 1
    template: tv
    rss: http://www.torlock.com/television/rss.xml

  saturdaynightlive:
    priority: 1
    template:
      - tv
    html:
      url: http://thepiratebay.se/search/saturday%20night%20live/{{i}}/99/208
      increment:
        from: 0
        to: 4
      title_from: url
      links_re: [ magnet ]
    manipulate:
      - title:
          from: url
          extract: '&dn=([^&](/^&)+)'
    archive: yes

  TheLibrariansUS:
    priority: 1
    template:
      - tv
    html:
      url: http://thepiratebay.se/search/The%20Librarians%20US/{{i}}/99/208
      increment:
        from: 0
        to: 2
      title_from: url
      links_re: [ magnet ]
    manipulate:
      - title:
          from: url
          extract: '&dn=([^&](/^&)+)'
    archive: yes

  thepiratebay_movies207:
    template: movies
    rss: http://rss.thepiratebay.se/207

  torlock_movies:
    template: movies
    rss: http://www.torlock.com/movies/rss.xml

  extratorrent_movies:
    template: movies
    rss: http://extratorrent.com/rss.xml?cid=4&type=last
     
  AddMovieTorrents:
    # it's a feed that scan a dir for torrent, it's like the watch thing of deluge
    # but this is better because flexget process the torrent, and then give it to deluge
    # so the files get the template TV and is processed. Of course i only put tv torrent here.
    # torrents that flexget didn't catch, or new serie i found and have already some ep out.
    listdir: /media/sdb2/Torrents/AddMovieTorrents
    accept_all: yes
    template: movies2

  seed_watchlist:
    # priority plugin is used so that this feed runs before the actual download feed
    priority: 1
    trakt_list:
      username: xxxxxxxx
      password: xxxxxxxxx
      api_key: xxxxxxxxxxxxxxxxxxxxxxxxxxx
      custom: Movies
    accept_all: yes
    queue_movies:
      quality: 720p-1080p hdtv-bluray

  moviesQueFeed:
    template: moviesQue
```

series.yml

```
series:
  - Fast Food Mania
  - Fish Tank Kings
  - Frys Planet Word
  - "The Librarians (US)"
```

### Attachments
* [My config.yml file (1.2.231)](/attachments/Cookbook/Users/paulpoco/config.yml)
* [My series.yml file (1.2.231)](/attachments/Cookbook/Users/paulpoco/series.yml)