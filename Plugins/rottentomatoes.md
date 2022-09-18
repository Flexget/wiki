---
title: rottentomatoes
description: 
published: true
date: 2022-09-18T05:12:30.430Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:11:21.398Z
---

# Filter Rotten Tomatoes
This plugin allows filtering based on Rotten Tomatoes score, rating and genres etc.
Results are cached so this doesn't cause unnecessary load to [Rotten Tomatoes](http://www.rottentomatoes.com).


**Notes:** 

 * If [Entry](/Entry) doesn't have `rt_id` present plugin will try to use Rotten Tomatoes's search function. This does not work on 100% of cases and in some rare cases it may even get wrong movie details.
 * To reject non Rotten Tomato compatible entries, use [rottentomatoes_lookup](/Plugins/rottentomatoes_lookup) and [require_field](/Plugins/require_field) with `rt_id`.
 * This plugin doesn't keep any track of accepted movies, if you want to prevent same movie being accepted multiple times use [seen_movies](/Plugins/seen_movies) plugin alongside.
 * The `require_certified_fresh` option will reject torrents even if they are accepted by other plugins.
 * You should [[http://developer.rottentomatoes.com/|create]] and use your own API key instead of the default, as Rotten Tomatoes limits the number of concurrent users per key. You can change the API key using [rottentomatoes_lookup](/Plugins/rottentomatoes_lookup)

### Example
```
rottentomatoes_lookup: rh8chjzp8vu6gnpwj88736uv # API key
rottentomatoes:
  min_critics_score: 75
  min_critics_rating: certified fresh
  reject_mpaa_ratings:
    - PG-13
```

### Full configuration
```
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
```