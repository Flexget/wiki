= Movie queue =

Accept movies based on a predefined queue. After a movie is in the queue, it will be forcibly accepted when seen, disregarding all other filters.

You need to manually add movies to the queue from the commandline.

== Queueing ==

{{{
flexget --movie-queue (add|del|list) [NAME|imdb_id=IMDB_ID|tmdb_id=TMDB_ID] [QUALITY] [FORCE]
}}}

If no quality is specified, it will add the movie with a quality of ANY. This will take the first matching download, regardless of quality.

See [wiki:Qualities qualities] for valid quality list.

Quality matches are no longer exact. There is "better than the quality specified" logic now added. Qualities above are from best to worst.

=== Examples ===

The following will queue [http://www.imdb.com/title/tt1038686/ Legion (2010)] with quality 720p

{{{
$ flexget --movie-queue add imdb_id=tt1038686 "720p bluray"
Added tt1038686 to queue with quality 720p bluray
}}}

You can also list the queue

{{{
$ flexget --movie-queue list
http://www.imdb.com/title/tt1038686 720p
}}}

== Enabling the filter ==

For movie-queue to look for matches in any feeds, there must be an entry in the configuration for that feed, matching the below.

{{{
movie_queue: yes
}}}

Movies get purged from queue when they reach output successfully.
