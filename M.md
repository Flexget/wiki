  movies search:

    priority: 10 # run after the movie queue fill task
    discover:
      what:
        - movie_list: watchlist
      from:
        - piratebay: yes
      interval: 7 days
    torrent_alive: 10 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
    list_match:
      from:
        - movie_list: watchlist
    transmission: yes # You could use another output plugin instead of this (deluge, download)