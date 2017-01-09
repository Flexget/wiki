this is my personal config.yml which does the following:

* downloads tv shows watchlisted on trakt.
* downloads movies watchlisted on imdb.
* uses deluge as the client to download torrents.
* uses multiple rss feeds per template.
* sends a push notification with pushbullet when a torrent is added to deluge.
* both tv shows and movies are downloaded in 720p resolution and h264 codec.

replace everything in ALL_CAPS with your relevant information and you should be good to go.

```
schedules:
  - tasks: [TV-SHOWS,MOVIES]
    interval:
      minutes: 15
  - tasks: [IMPORT-MOVIES]
    interval:
      minutes: 120    

templates:
  tv:
    deluge:
      host: DELUGE_HOST
      port: DELUGE_PORT
      username: DELUGE_USERNAME
      password: DELUGE_PASSWORD
      path: PATH_TO_STORE_TV_SHOWS
    configure_series:
      settings:
        quality: webdl|hdtv|webrip h264 720p
        propers: no
      from:
        trakt_list:
          username: TRAKT_USERNAME
          list: watchlist
          type: shows
          strip_dates: yes
    regexp:
      from: title
      reject:
        - msd
        - afg
        - line
    content_size:
      min: 400
      max: 3000
      strict: no
    pushbullet:
      apikey: PUSHBULLET_API_KEY
      title: "[F] {{series_name}} {{series_id}}"
      body: "{{title}}\n\nSize: {{content_size}}MB"
    inputs:
      - rss:
          url: A_RSS_URL_TO_GET_TV_SHOWS_FROM
          all_entries: no
      - rss:
          url: ANOTHER_RSS_URL_TO_GET_TV_SHOWS_FROM
          all_entries: no

  movie:
    deluge:
      host: DELUGE_HOST
      port: DELUGE_PORT
      username: DELUGE_USERNAME
      password: DELUGE_PASSWORD
      path: PATH_TO_STORE_MOVIES
    quality: bluray|webdl h264 720p
    imdb_lookup: yes
    list_match:
      from:
        - movie_list: mymovies
    regexp:
      from: title
      reject:
        - msd
        - afg
        - line
        - hc
        - korsub
    content_size:
      min: 1500
      max: 8000
      strict: no
    pushbullet:
      apikey: PUSHBULLET_API_KEY
      title: "[F] {{imdb_name}}"
      body: "{{title}}\n\n{{imdb_url}}\n\nSize: {{content_size}}MB"
    inputs:
      - rss:
          url: A_RSS_URL_TO_GET_MOVIES_FROM
          all_entries: no
      - rss:
          url: ANOTHER_RSS_URL_TO_GET_MOVIES_FROM
          all_entries: no

tasks:
  TV-SHOWS:
    template: tv
    priority: 1
    
  IMPORT-MOVIES:
    imdb_list:
      login: IMDB_USER_EMAIL
      password: IMDB_PASSWORD
      list: watchlist
    accept_all: yes
    list_add:
      - movie_list: mymovies
    priority: 2

  MOVIES:
    template: movie
    priority: 3
```