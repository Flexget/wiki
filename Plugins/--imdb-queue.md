= IMDb queue =

Accept movies based on a predefined queue. After a movie is in the queue, it will be forcibly accepted when seen, disregarding all other filters.

You need to manually add movies to the queue from the commandline.

=== Usage ===

{{{
flexget --imdb-queue (add|del|list) [IMDB_URL] [QUALITY]
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