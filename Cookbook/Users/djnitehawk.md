this is my personal config.yml which does the following:

* download tv shows that's in a custom trakt.tv list.
* download movies watchlisted in my imdb a/c.
* uses deluge as the client to download torrents.
* uses multiple rss feeds per template.
* sends a push notification with pushbullet when a torrent is added to transmission.
* both tv shows and movies are downloaded in 720p resolution.

replace everything in ALL_CAPS with your relevant information and you should be good to go.

{{{
schedules:
  - tasks: '*'
    interval:
      minutes: 10

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
        quality: hdtv|webdl xvid|divx|h264 720p
        propers: no
      from:
        trakt_list:
          username: TRAKT_USERNAME
          api_key: TRAKT_API_KEY
          custom: A_CUSTOM_TRAKT_LIST_TO_GET_SERIES_NAMES_FROM
          strip_dates: yes
    regexp:
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
          url: http://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_TV_SHOWS
          all_entries: no
      - rss:
          url: http://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP
          all_entries: no

  movie:
    deluge:
      host: localhost
      port: DELUGE_PORT
      username: DELUGE_USERNAME
      password: DELUGE_PASSWORD
      path: A_PATH_TO_STORE_MOVIES
    movie_queue: yes
    proper_movies: no
    regexp:
      reject:
        - msd
        - afg
        - line
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
          url: http://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_MOVIES
          all_entries: no
      - rss:
          url: http://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP
          all_entries: no

tasks:
  TV-SHOWS:
    template: tv
    priority: 1

  IMPORT-MOVIES:
    imdb_list:
      user_id: IMDB_USER_ID
      list: watchlist
    accept_all: yes
    queue_movies:
      quality: bluray|webdl xvid|divx|h264 720p
    priority: 2

  MOVIES:
    template: movie
    priority: 3
}}}