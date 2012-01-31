= Movie queue =

Accept movies based on a predefined queue. After a movie is in the queue, it will be forcibly accepted when seen, disregarding all other filters.

You need to manually add movies to the queue from the commandline, or set up a separate feed with the [wiki:Plugins/queue_movies queue_movies] plugin.

== Related plugins ==

 * [wiki:Plugins/proper_movies proper_movies]
 * [wiki:Plugins/seen_movies seen_movies]

== Queueing ==

{{{
flexget --movie-queue (add|del|list) [NAME|imdb_id=IMDB_ID|tmdb_id=TMDB_ID] [QUALITY] [FORCE]
}}}

If no quality is specified, it will add the movie with a quality of ANY. This will take the first matching download, regardless of quality.

See [wiki:Qualities qualities] for valid quality list.

Quality matches are no longer exact. There is "better than the quality specified" logic now added. Qualities above are from best to worst.

If force flag is given (values: yes|no) it will cause movie to be marked as immortal and forced trough other possible filters.

=== Examples ===

The following will queue [http://www.imdb.com/title/tt1038686/ Legion (2010)] with quality 720p

{{{
$ flexget --movie-queue add imdb_id=tt1038686 "720p bluray"
Added tt1038686 to queue with quality 720p bluray
}}}

Adding with name works too, if name can be queried from imdb/tmdb successfully.

{{{
$ flexget --movie-queue add legion "720p bluray"
}}}


You can also list the queue

{{{
$ flexget --movie-queue list
http://www.imdb.com/title/tt1038686 720p bluray
}}}

== Enabling the filter ==

Simply adding movies to queue will not cause them to be downloaded, you will also need to tell !FlexGet which feeds the queue is used on. This is done simply by enabling `movie_queue` on them.

{{{
movie_queue: yes
}}}

Since this will also cause imdb and/or tmdb queries it would be best to use it on feeds where there are only movies.

Movies get purged from queue when they reach output successfully.

== Clearing the movie list ==

In the event that you have accidentally managed to fill your movie_queue with a bunch of movies (perhaps with wrong settings), this little (linux) snippet will clear the list while we wait for a --movie clear command :)


{{{
for i in `flexget --movie-queue list|grep tt|cut -d" " -f1`; do flexget --movie-queue del $i; done
}}}

