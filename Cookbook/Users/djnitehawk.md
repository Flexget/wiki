this is my personal config.yml which does the following:

* downloads tv shows watchlisted on trakt.
* downloads movies watchlisted on imdb.
* uses deluge as the client to download torrents.
* uses multiple rss feeds per template.
* sends a push notification with pushbullet when a torrent is added to deluge.
* both tv shows and movies are downloaded in 720p resolution.

replace everything in ALL_CAPS with your relevant information and you should be good to go.

{{{
schedules:
  - tasks: '*'
    interval:
      minutes: 15

templates:
  tv:
    deluge:
      host: localhost
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
          url: https://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_TV_SHOWS
          all_entries: no
      - rss:
          url: https://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP
          all_entries: no

  movie:
    deluge:
      host: localhost
      port: DELUGE_PORT
      username: DELUGE_USERNAME
      password: DELUGE_PASSWORD
      path: PATH_TO_STORE_MOVIES
    quality: bluray|webdl h264 720p
    imdb_lookup: yes
    list_accept:
      - imdb_list:
          login: IMDB_USERNAME
          password: IMDB_PASSWORD
          list: watchlist
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
          url: https://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_MOVIES
          all_entries: no
      - rss:
          url: https://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP
          all_entries: no

tasks:
  TV-SHOWS:
    template: tv

  MOVIES:
    template: movie
}}}