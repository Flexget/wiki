= Movies Timeframe =

The [wiki:Plugins/series series] plugin has timeframe functionality which allows download to wait certain time for better quality to appear. There isn't this kind of plugin for movies, but it can be achieved with some clever use of [wiki:Plugins/delay delay] plugin.

'''Example:'''

{{{
preset:
  movies:
    imdb:
      min_score: 6.2
      min_votes: 5000
  seen_movies: yes
  download: ~/torrents/movies/

feeds:

  feed-1080p:
    priority: 1
    rss: http://example.com/feed.rss
    quality: 1080p
    delay: 10 hours
  
  feed-720p:
    priority: 2
    rss: http://example.com/feed.rss
    quality: 720p
    delay: 10 hours
}}}

This is effectively 10 hour timeframe for 1080p and if the movie is not found by then it will fall back to 720p.

Don't be worried about requesting the same feed twice, it is cached and the second feed does not request it again.
