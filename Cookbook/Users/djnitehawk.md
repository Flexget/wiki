this is my personal config.yml which does the following:

* download tv shows that's in a custom trakt.tv list.
* download movies watchlisted in my imdb a/c.
* uses transmission as the client to download torrents.
* uses multiple rss feeds per template.
* sends a push notification with pushbullet when a torrent is added to transmission.
* both tv shows and movies are downloaded in 720p resolution.

replace everything in ALL_CAPS with your relevant information and you should be good to go.

{{{
templates:
  tv:
    transmission:
      host: localhost
      port: TRANSMISSION_PORT
      username: TRANSMISSION_USERNAME
      password: TRANSMISSION_PASSWORD
      addpaused: no
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
    content_size:
      min: 400
      max: 3000
      strict: no
    pushbullet:
      apikey: PUSHBULLET_API_KEY
      title: "{{series_name}} {{series_id}}"
      body: "{{title}}\n\nSize: {{content_size}}MB"
    inputs:
      - rss: http://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_TV_SHOWS
      - rss: http://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP

  movie:
    transmission:
      host: localhost
      port: TRANSMISSION_PORT
      username: TRANSMISSION_USERNAME
      password: TRANSMISSION_PASSWORD
      addpaused: no
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
      title: "{{imdb_name}}"
      body: "{{title}}\n\n{{imdb_url}}\n\nSize: {{content_size}}MB"
    inputs:
      - rss: http://PRIVATE_OR_PUBLIC_TORRENT_RSS_FEED_FOR_MOVIES
      - rss: http://ANOTHER_TORRENT_RSS_FEED_AS_A_BACKUP

tasks:
  TV-SHOWS:
    template: tv
    priority: 1

  IMPORT-MOVIES:
    imdb_list:
      username: IMDB_USERNAME
      password: IMDB_PASSWORD
      list: watchlist
    accept_all: yes
    queue_movies:
      quality: dvdrip|bluray|webdl xvid|divx|h264 720p
    priority: 2

  MOVIES:
    template: movie
    priority: 3
}}}