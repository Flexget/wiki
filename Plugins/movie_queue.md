= Movie queue =

Maintains internal list of movies with quality information and accepts them when they're seen on the task.
You need to manually add movies to the queue from the commandline, or set up a separate task with the [wiki:Plugins/queue_movies queue_movies] plugin which allows automatic queueing from numerous sources like imdb watchlist etc.

== Related plugins ==

 * [wiki:Plugins/proper_movies proper_movies]
 * [wiki:Plugins/seen_movies seen_movies]

== Queueing ==

{{{
flexget movie-queue (add|del|forget|list|downloaded|clear) [NAME|imdb_id=IMDB_ID|tmdb_id=TMDB_ID] [QUALITY]
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

== Enabling the filter ==

Simply adding movies to queue will not cause them to be downloaded, you will also need to tell !FlexGet which tasks the queue is used on. This is done simply by enabling `movie_queue` on them.

{{{
movie_queue: yes
}}}

Since this will also cause imdb and/or tmdb queries it would be best to use it on feeds where there are only movies.

Movies get moved from queue to the downloaded list when they reach output successfully.

== Checking what was downloaded ==

This command will tell you what the movie_queue list has downloaded.

{{{
$ flexget movie-queue downloaded
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
||list||None||Lists all wanted movies in the queue.||
||downloaded||None||List all queue movies that have already been acquired.||
||clear||None||Removes all movies from the pending queue.||
