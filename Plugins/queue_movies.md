= Queue Movies =
This plugin adds a movie to your [wiki:Plugins/movie_queue movie_queue] for each accepted entry in a feed.

'''Example:'''
Useful with the imdb_watchlist plugin to add all movies in your imdb watchlist to your movie queue.
{{{
  imdb_watchlist:
    username: myimdbuser
    password: mypass
  accept_all: yes
  queue_movies: yes
}}}