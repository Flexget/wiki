= IMDb queue =

Accept movies based on a predefined queue. After a movie is in the queue, it will be forcibly accepted when seen, disregarding all other filters.

You need to manually add movies to the queue from the commandline.

=== Example ===

{{{
flexget --imdb-queue=http://www.imdb.com/title/tt1038686/
}}}

You can also list the queue

{{{
flexget --imdb-queue-list
}}}

'''TODO''': 
 * Minimum(/maximum?) quality filtering
 * Filter by group, default to any group