= Fill movie_queue from trakt.tv or IMDb watchlist =

This task will add movies from [http://trakt.tv trakt.tv] and/or [http://imdb.com IMDb] watchlists to your [wiki:Plugins/movie_queue movie_queue]. This is not intended to download anything, just fill the !FlexGet movie queue from there. You will have to have another task with the [wiki:Plugins/movie_queue movie_queue] plugin to do the actual downloading. You can remove either the [wiki:Plugins/imdb_list imdb_list] or [wiki:Plugins/trakt_list trakt_list] plugin from this recipe if you do not want to use that particular site.

{{{
tasks:
  watchlist:
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
    seen: local  # We don't want accepted movies on this feed to affect actual download feed
    queue_movies:
      quality: 720p bluray
      force: no
}}}

'''NOTE:''' Make sure you don't have download/deluge/transmission plugin in this task, (or in a global preset,) you aren't actually downloading anything here.

== Plugins used ==

||=Plugin=||=Reason=||
||[wiki:Plugins/priority priority]||Run the task early, before other tasks that may do downloading||
||[wiki:Plugins/interval interval]||Reasonable update frequency so that sites are not overloaded||
||[wiki:Plugins/trakt_list trakt_list]||Watch list source||
||[wiki:Plugins/imdb_list imdb_list]||Watch list source||
||[wiki:Plugins/accept_all accept_all]||We want to add all items to the queue||
||[wiki:Plugins/queue_movies queue_movies]||Output which adds entries to our movie queue||