= IMDb queue =

Accept movies based on a predefined queue. After a movie is in the queue, it will be forcibly accepted when seen, disregarding all other filters.

You need to manually add movies to the queue from the commandline.

=== Usage ===

{{{
flexget --imdb-queue (add|del|list) [IMDB_URL] [QUALITY]
}}}

If no quality is specified, it will add the movie with a quality of ANY. This will take the first matching download, regardless of quality.

Recognized qualities are 1080p, 1080, 720p, 720, hr, dvd, bdrip, dvdrip, 480p, 480, bdscr, dvdscr, hdtv, pdtv, dsr, dsrip, r5, cam, unknown, ANY

Quality matches are EXACT. There is no "better than the quality specified" logic.

For imdb-queue to look for matches in any feeds, there must be an entry in the configuration for that feed, matching the below.

{{{
imdb_queue: yes
}}}

=== Examples ===

The following will queue [http://www.imdb.com/title/tt1038686/ Legion (2010)] with quality 720p

{{{
$ flexget --imdb-queue add http://www.imdb.com/title/tt1038686/ 720p
Added tt1038686 to queue with quality 720p
}}}


You can also list the queue

{{{
$ flexget --imdb-queue list
http://www.imdb.com/title/tt1038686 720p
}}}