= Seed movie_queue from trakt.tv/IMDb watchlist =
This feed will cause all of the movies you add to your [http://trakt.tv trakt.tv] and/or [http://imdb.com IMDb] watchlist to your [wiki:Plugins/movie_queue movie_queue]. It will not actually download anything, you will have to set up another feed with the [wiki:Plugins/movie_queue movie_queue] plugin to do the actual downloading. You can remove the [wiki:Plugins/imdb_list imdb_list] or [wiki:Plugins/trakt_list trakt_list] plugin from this recipe if you do not want to use that particular site.
{{{
feeds:
  seed_watchlist:
    # priority plugin is used so that this feed runs before the actual download feed
    priority: 1
    interval: 2 hours
    trakt_list:
      api_key: myapikey
      username: myusername
      movies: watchlist
    imdb_list:
      list: watchlist
      username: me@somewhere.com
      password: mypassword
    accept_all: yes
    queue_movies:
      quality: 720p bluray
      force: no
}}}
Plugins used: [wiki:Plugins/priority priority], [wiki:Plugins/interval interval], [wiki:Plugins/trakt_list trakt_list], [wiki:Plugins/imdb_list imdb_list], [wiki:Plugins/accept_all accept_all], [wiki:Plugins/queue_movies queue_movies]