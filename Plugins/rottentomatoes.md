= Filter Rotten Tomatoes =

This plugin allows filtering based on Rotten Tomatoes score, rating and genres etc.
Results are cached so this doesn't cause unnecessary load to [http://www.rottentomatoes.com Rotten Tomatoes].


'''Notes:''' 

 * If [wiki:Entry] doesn't have `rt_id` present plugin will try to use Rotten Tomatoes's search function. This does not work on 100% of cases and in some rare cases it may even get wrong movie details.
 * To reject non imdb compatible entries, use [wiki:Plugins/rottentomatoes_lookup rottentomatoes_lookup] and [wiki:Plugins/require_field require_field] with `rt_id`.
 * This plugin doesn't keep any track of accepted movies, if you want to prevent same movie being accepted multiple times use [wiki:Plugins/seen_movies seen_movies] plugin alongside.
 * The `require_certified_fresh` option will reject torrents even if they are accepted by other plugins.

=== Example ===

{{{
rotten_tomatoes:
  min_critics_score: 75
  require_certified_fresh: yes
  reject_mpaa_ratings:
    - PG-13
}}}

=== Full configuration ===

{{{
        Note: All parameters are optional. Some are mutually exclusive.

        min_critics_score: <num>
        min_audience_score: <num>
        min_average_score: <num>
        require_certified_fresh: <num>
        min_year: <num>
        max_year: <num>

        # reject if genre contains any of these
        reject_genres:
            - genre1
            - genre2

        # accept movies with any of these actors
        accept_actors:
            - actor1
            - actor2

        # reject movie if it has any of these actors
        reject_actors:
            - actor3
            - actor4

        # accept all movies by these directors
        accept_directors:
            - director1

        # reject movies by these directors
        reject_directors:
            - director2

        # reject movies with any of these ratings
        reject_mpaa_ratings:
            - PG-13
            - R
            - X

        # accept movies with only these ratings
        accept_mpaa_ratings:
            - PG
            - G
}}}