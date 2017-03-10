After reading other users config and Flexget code, I have write my own config and prepare some PR to search movies in Spanish webs.

I have split my config in several files and include in the main config


**Flexget:**
+ 2.10.12.dev
+ Latest release: 2.10.11

## Main config


```
variables: secretfile.yml
templates:
  torrent_server:
    transmission:
      host: localhost
      port: 9091
      username: "{? transmission.usr ?}"
      password: "{? transmission.pwd ?}"
  avisos_tarea:
    notify:
      task:
        via:
          - email:
              from: "{? email.from ?}"
              to: "{? email.to ?}"
              smtp_host: smtp.gmail.com
              smtp_port: 587
              smtp_username: "{? email.smtp_username ?}"
              smtp_password: "{? email.smtp_password ?}"
              smtp_tls: yes
          - telegram:
              bot_token: "{? telegram.token ?}"
              parse_mode: markdown
              #parse_mode: html
              recipients:
                - username: "{? telegram.user ?}"
  avisos_error:
    notify:
      abort:
        via:
          - email:
              from: "{? email.from ?}"
              to: "{? email.to ?}"
              smtp_host: smtp.gmail.com
              smtp_port: 587
              smtp_username: "{? email.smtp_username ?}"
              smtp_password: "{? email.smtp_password ?}"
              smtp_tls: yes

schedules:
  - tasks: [mis_series, animeindexfs, nyaafs, minglongfs, nyaaevermore, frozenpuya]
    schedule:
      minute: 45
      hour: 7,11,15,19,23
  - tasks: [watchlist, bajar_pelis]
    schedule:
      minute: 30
      hour: 12

web_server:
  bind: 0.0.0.0 # IP V4
  port: 8290 # Valid port number
  ssl_certificate: 'fullchain.pem' 
  ssl_private_key: 'privkey.pem'
  web_ui: yes # Web-UI can optionally be disabeled, only API will run

tasks:
  mis_series:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include: 
#      - series_divxatope.yml
      - series_newpct.yml
  animeindexfs:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include:
      - animes_fs_animeindex.yml
  nyaafs:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include:
      - animes_fs_nyaa.yml
    cfscraper: yes
  minglongfs:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include:
      - animes_fs_minglong.yml
  nyaaevermore:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include:
      - animes_evermore_nyaa.yml
  frozenpuya:
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
    include:
      - animes_puya_frozen.yml
  watchlist:
    priority: 1
    interval: 2 hours
    imdb_watchlist:
      user_id: "{? imdb.user_id ?}"
      list: watchlist
      force_language: es-es
    accept_all: yes
    list_add:
      - movie_list: wanted_movies
    template:
      - avisos_tarea
  bajar_pelis:
    priority: 10
    discover:
      what:
        - movie_list: wanted_movies
#        - emit_movie_queue: yes
      from:
#        - divxatope: yes
        - newpct: yes
#        - divxatope:
#            category: all
#        - elitetorrent:
#            category: all
#        - torrentdownloadws: true
#        - kat:
#            category: movies
#            verified: no
#        - piratebay:
#            category: video
#            sort_by: default
#        - torrentz: verified
      interval: 1 hours
      release_estimations:
        optimistic: 7 days
    imdb_lookup: yes
    tmdb_lookup: yes
    trakt_lookup: yes
    quality:
      - dvdrip+
      - hdrip
      - hdtv # Make sure no screeners or cams are downloaded
    set:
      path: /media/269c2dba-2000-495f-9bd8-e09c36b16f4e/pelis
    template:
      - torrent_server
      - avisos_tarea
      - avisos_error
#      - proxyy
    list_match:
      from:
        - movie_list: wanted_movies
    regexp:
      reject:
        - 'sub[s][\s\._]'
        - '[Ll]atino'
        - '[Ss]creener'
        - '[Ss]creener':
            from: url
        - Screeener
        - Screeener:
            from: url
        - 3D
      from: title
      reject_excluding:
        - '[Rr]ip|HDTV'
#EOF      

```

## DivXATope


```
rss:
  url: http://divxatope.com/feeds.xml
series:
  settings:
    normales:
      ep_regexp:
        - Cap.(\d+)(\d\d)
      quality: hdtv <720p
      path: /media/269c2dba-2000-495f-9bd8-e09c36b16f4e/series/{{series_name}}
  normales:
    - Alli abajo
    - Arrow
    - Westworld
regexp:
  reject:
    - V.O.:
        from: title
```

## NewPCT
```
rss:
  url: http://www.newpct.com/feed/
  link: link
series:
  settings:
    normales:
      ep_regexp:
        - Cap.(\d+)(\d\d)
      quality: hdtv <720p
      path: /media/269c2dba-2000-495f-9bd8-e09c36b16f4e/series/{{series_name}}
  normales:
    - Alli abajo
    - Arrow
    - Westworld
regexp:
  reject:
    - V.O.:
        from: title
```