= Movie queue =

Manages an internal list of movies with quality information. Allows you to accept movies, add movies to the queue, or remove movies from the queue when they are seen on the task. You also have the ability to manually add movies to the queue from the command line.

== Related plugins ==

 * [wiki:Plugins/proper_movies proper_movies]
 * [wiki:Plugins/seen_movies seen_movies]

== Queueing ==

{{{
flexget movie-queue (add|del|forget|list|clear) [NAME|imdb_id=IMDB_ID|tmdb_id=TMDB_ID] [QUALITY]
}}}

If no quality is specified, it will add the movie with a quality of ANY. This will take the first matching download, regardless of quality.

See [wiki:Qualities qualities] for valid quality requirements.

=== Examples ===

The following will queue [http://www.imdb.com/title/tt1038686/ Legion (2010)] with quality 720p

{{{
$ flexget movie-queue add legion "720p bluray"
}}}

Alternatively you can queue by imdb_id or tmdb_id.

{{{
$ flexget movie-queue add imdb_id=tt1038686 "720p bluray"
Added tt1038686 to queue with quality 720p bluray
}}}

You can also list the queue

{{{
$ flexget movie-queue list
http://www.imdb.com/title/tt1038686 720p bluray
}}}


== !Adding/Removing using Tasks ==
This plugin is an output plugin that adds or removes a movies to your movie queue for each accepted entry in a task. 

With this you could for example queue all movies in your imdb watchlist by creating following task.

'''Example:'''

{{{
tasks:
  queue_from_imdb:
    imdb_list:
      username: myimdbuser
      password: mypass
      list: watchlist
    accept_all: yes
    movie_queue: add              # you could also use `remove` if you wanted to remove the item from your queue
}}}

Or from RSS feed.

'''Example:'''

{{{
tasks:
  queue_from_foobar:
    rss: http://foobar.com/rss.xml # input
    accept_all: yes                # filter which accepts everything
    movie_queue: add               # output entries to movie queue (with quality any)
}}}

These are not tasks in traditional !FlexGet sense as they don't download anything. Instead they are more like utility tasks.

Queue movies will work best with entries containing imdb_id/url or tmdb, if they're not available it will try to get them on it's own. Relying on this will mean that some of the entries may not be added to the movie queue.


=== Options ===

You can also specify options for items being added to the movie queue. Most people will not want to use this option. Instead, the [wiki:Plugins/quality quality] plugin should be used in your download task.

{{{
movie_queue:
  action: add
  quality: 720p+ bluray
}}}

See [wiki:Qualities qualities] page for valid quality requirements.


== Enabling the filter ==

Simply adding movies to queue will not cause them to be downloaded, you will also need to tell !FlexGet which tasks the queue is used on. This is done simply by enabling `movie_queue` on them.

{{{
movie_queue: accept
}}}

Since this will also cause imdb and/or tmdb queries it would be best to use it on feeds where there are only movies.

Movies get moved from queue to the downloaded list when they reach output successfully.

== Checking what was downloaded ==

This command will tell you what the movie_queue list has downloaded.

{{{
$ flexget movie-queue list downloaded
}}}

If you would like to get a different copy of a movie that has already been downloaded, you can use the forget command to remove the downloaded flag and allow another copy to be accepted.
{{{
$ flexget movie-queue forget "The Movie"
}}}

== Clearing the movie Queue list ==

In the event that you have accidentally managed to fill your movie_queue with a bunch of movies (perhaps with wrong settings), this command will clear the queue list, but leaves intact the downloaded list.


{{{
$ flexget movie-queue clear
}}}

== Command Line Interface ==

The movie queue can be controlled via the command line interface. 

{{{
flexget movie-queue <ACTION> [PARAMETERS]
}}}

The following actions are supported. {{{<IDENTIFIER>}}} can be either the title of the movie, imdb id, or for tmdb id. Tmdb id must be in the form tmdb_id=12345.

||'''Action'''||'''Parameters'''||'''Description'''||
||add||<IDENTIFIER> [QUALITY]||Add a movie to the queue.||
||del||<IDENTIFIER>||Remove a movie from the queue.||
||forget||<IDENTIFIER>||Mark an already downloaded queue item as wanted again.||
||list||waiting|downloaded||Lists all waiting/downloaded movies in the queue.||
||clear||None||Removes all movies from the pending queue.||
