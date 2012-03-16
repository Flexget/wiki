This recipe aims to allow adding of movies as simple as adding a movie to your trakt.tv watchlist.

How to create a feed that queues movies from entries in your [http://trakt.tv trakt.tv] watchlist is explained in this [wiki:Cookbook/Movies/TraktList cookbook]. So that part won't be explained in detail here.

This cookbook goes one step further and also uses the [wiki:Plugins/discover discover plugin] in conjunction with the [wiki:Plugins/search_rss search_rss] plugin to dynamically create feeds from which entries can be harvested. The [wiki:Plugins/torrent_alive torrent_alive plugin] cycles the feed until it finds an entry with an acceptalbe amount of seeds. This is required since most of the query based feeds do not guarantee that the torrents have enough seeds or any kind of sorting.
{{{
feeds:
  #feed to pull movies from trakt.tv watchlist and add to the movie queue
  trakt_movie_queue_fill:
    priority: 1
    trakt_list:
      username: myusername
      api_key: myapikey
      movies: watchlist
    accept_all: yes
    queue_movies:
      quality: dvdrip
      force: no

  # feed that automatically generates an rss feed based on entries from the movie_queue
  isohuntmovies search:
    priority: 10
    preset:
      - dlvector
    torrent_alive: 10
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - isohunt: movies
        - torrentz
      type: movies
    movie_queue: yes
    transmission:
      # localhost is whitelisted so doesn't need password
      host: localhost
      port: 9091
      ratio: 1.50
      removewhendone: True
      path: /mnt/cloud/share/film/{{movie_name}}/{{quality}}
    trakt_acquired:
      username: myusername
      password: mypassword
      api_key: myapikey
      type: movies
}}}
Plugins used: [wiki:Plugins/preset preset], [wiki:Plugins/priority priority], [wiki:Plugins/set set], [wiki:Plugins/transmission transmission], [wiki:Plugins/trakt_list trakt_list], [wiki:Plugins/trakt_acquired trakt_acquired], [wiki:Plugins/accept_all accept_all], [wiki:Plugins/queue_movies queue_movies], [wiki:Plugins/torrent_alive torrent_alive], [wiki:Plugins/discover discover] using [wiki:Searches search plugins] [wiki:Searches/isohunt isohunt] and torrentz.