Note: All parameters are optional. Some are mutually exclusive.

        min_critics_score: <num>
        min_audience_score: <num>
        min_average_score: <num>
        min_critics_rating: <rotten, fresh, or certified fresh>
        min_audience_rating: <upright or spilled>
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