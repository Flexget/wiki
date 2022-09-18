---
title: imdb
description: 
published: true
date: 2022-09-18T05:12:30.430Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:06:22.850Z
---

# Filter IMDB
This module allows filtering based on IMDB score, votes and genres etc.
Results are cached so this doesn't cause unnecessary load to [imdb](http://www.imdb.com).


**Notes:** 

 * If [Entry](/Entry) doesn't have `imdb_id` present plugin will try to use imdb's search function. This does not work on 100% of cases and in some rare cases it may even get wrong movie details.
 * To reject non imdb compatible entries, use [require_field](/Plugins/require_field) plugin on the 'imdb_id' field.
 * This plugin doesn't keep any track of accepted movies, if you want to prevent same movie being accepted multiple times use [seen_movies](/Plugins/seen_movies) plugin alongside.

### Example
```
imdb:
  min_score: 6.2
  min_votes: 5000
  reject_genres:
    - horror
```

### Full configuration
```
Note: All parameters are optional. Some are mutually exclusive.

        min_score: <num>
        min_votes: <num>
        min_year: <num>
        max_year: <num>

        # reject if genre contains any of these
        reject_genres:
            - genre1
            - genre2

        # reject if language contain any of these
        reject_languages:
            - language1

        # accept only these as primary language
        accept_languages:
            - language1

        # accept movies with any of these actors
        accept_actors:
            - nm0004695
            - nm0004754

        # reject movie if it has any of these actors
        reject_actors:
            - nm0001191
            - nm0002071

        # accept all movies by these directors
        accept_directors:
            - nm0000318

        # reject movies by these directors
        reject_directors:
            - nm0093051

        # accept all movies by these writers
        accept_writers:
            - nm0000318

        # reject movies by these writers
        reject_writers:
            - nm0093051
        
        # reject movies/TV shows with any of these ratings
        reject_mpaa_ratings:
            - PG_13
            - R
            - X
            
        # accept movies/TV shows with only these ratings
        accept_mpaa_ratings:
            - PG
            - G
            - TV_Y
```

Notice that the MPAA ratings all have _ instead of - and TV ratings are also applicable. "NONE" is also an acceptable rating, and will catch anything without an MPAA rating attached.