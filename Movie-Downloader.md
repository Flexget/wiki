tasks:
  #task to pull movies from trakt.tv watchlist and add to the movie list
  watchlist:
    priority: 1
    trakt_list:  # You can also use imdb_list
      account: my_acc_name
      list: watchlist
    accept_all: yes
    seen: local  # We don't want accepted movies on this feed to affect actual download feed
    list_add:
      - movie_list: watchlist  # you can call this whatever you want

  # task that automatically downloads movies from the movie_list
  movies search:
    trakt_lookup: yes  # can also use imdb_lookup or tmdb_lookup
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
    download: Users/petersterling/Desktop/torrents