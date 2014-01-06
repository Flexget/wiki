This recipe aims to allow adding of movies as simple as adding a movie to your trakt.tv watchlist.

How to create a task that queues movies from entries in your [http://trakt.tv trakt.tv] watchlist is explained in this [wiki:Cookbook/Movies/TraktList cookbook]. This is the 'trakt_movie_queue_fill' task in this recipe. So that part won't be explained in detail here.

This recipe goes one step further and also uses the [wiki:Plugins/discover discover plugin]] to dynamically search for the desired movies. The [wiki:Plugins/torrent_alive torrent_alive plugin] is used to reject results that do not have at least a minimum number of seeds, which usually improves the quality of the results.

{{{
tasks:
  #task to pull movies from trakt.tv watchlist and add to the movie queue
  trakt_movie_queue_fill:
    priority: 1 # run before the movie search task
    trakt_list:
      username: myusername
      api_key: myapikey
      movies: watchlist
    accept_all: yes
    queue_movies: yes

  # task that automatically generates an rss feed based on entries from the movie_queue
  movies search:
    priority: 10 # run after the movie queue fill task
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - isohunt: movies
        - torrentz: verified
      interval: 7 days
    torrent_alive: 10 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
    movie_queue: yes
    transmission: yes # You could use another output plugin instead of this (deluge, download)
}}}
Plugins used: [wiki:Plugins/template template], [wiki:Plugins/priority priority], [wiki:Plugins/set set], [wiki:Plugins/transmission transmission], [wiki:Plugins/trakt_list trakt_list], [wiki:Plugins/trakt_acquired trakt_acquired], [wiki:Plugins/accept_all accept_all], [wiki:Plugins/queue_movies queue_movies], [wiki:Plugins/torrent_alive torrent_alive], [wiki:Plugins/discover discover] using [wiki:Searches search plugins] [wiki:Searches/isohunt isohunt] and torrentz.