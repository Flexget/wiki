= Rotten Tomatoes List =

Emits an entry for each movie in a [http://www.rottentomatoes.com Rotten Tomatoes] list.

=== Configuration ===
{{{
    rottentomatoes_list:
        dvds:
          - top_rentals
          - upcoming
        movies:
          - box_office
}}}
	
''' Possible lists are '''
* dvds:
 * top_rentals
 * current_releases
 * new_releases
 * upcoming
* movies
 * box_office
 * in_theaters
 * opening
 * upcoming