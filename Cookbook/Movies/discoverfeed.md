# Dowload movies with discover
This recipe aims to allow adding of movies as simple as adding a movie to your trakt.tv watchlist.

How to create a task that adds movies from 3rd party sources to your movie_list is explained in this [cookbook](/Cookbook/Movies/TraktList).

This recipe goes one step further and also uses the [discover plugin](/Plugins/discover) to dynamically search for the desired movies. The [torrent_alive plugin](/Plugins/torrent_alive) is used to reject results that do not have at least a minimum number of seeds, which usually improves the quality of the results.

```
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
    transmission: yes # You could use another output plugin instead of this (deluge, download)
```
Plugins used: [priority](/Plugins/priority), [transmission](/Plugins/transmission), [trakt_list](/Plugins/trakt_list),[trakt_lookup](/Plugins/trakt_lookup), [accept_all](/Plugins/accept_all), [movie_list](/Plugins/List/movie_list), [list_match](/Plugins/List/list_match), [seen](/Plugins/seen), [torrent_alive](/Plugins/torrent_alive), [discover](/Plugins/discover) using [search plugin](/Searches) [piratebay](/Searches/piratebay).