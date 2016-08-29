# Fill movie_queue from trakt.tv or IMDb watchlist
This task will add movies from [trakt.tv](http://trakt.tv) and/or [IMDb](http://imdb.com) watchlists to your [movie_queue](/Plugins/movie_queue). This is not intended to download anything, just fill the FlexGet movie queue from there. You will have to have another task with the [movie_queue](/Plugins/movie_queue) plugin to do the actual downloading. You can remove either the [imdb_list](/Plugins/imdb_list) or [trakt_list](/Plugins/trakt_list) plugin from this recipe if you do not want to use that particular site.

```
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
    queue_movies: yes
```

**NOTE:** Make sure you don't have download/deluge/transmission plugin in this task, (or in a global template,) you aren't actually downloading anything here.

## Plugins used

| Plugin | Reason |
| --- | --- |
| [priority](/Plugins/priority) | Run the task early, before other tasks that may do downloading |
| [interval](/Plugins/interval) | Reasonable update frequency so that sites are not overloaded |
| [trakt_list](/Plugins/trakt_list) | Watch list source |
| [imdb_list](/Plugins/imdb_list) | Watch list source |
| [accept_all](/Plugins/accept_all) | We want to add all items to the queue |
| [queue_movies](/Plugins/queue_movies) | Output which adds entries to our movie queue||