= Queue Movies =

This plugin is an output plugin that adds a movies to your [wiki:Plugins/movie_queue movie_queue] for each accepted entry in a task. This plugin alone is not useful. To accept the queued movies you will need a task with [wiki:Plugins/movie_queue movie_queue] in it.

With this you could for example queue all movies in your imdb watchlist by creating following feed.

'''Example:'''

{{{
tasks:
  queue_from_imdb:
    imdb_list:
      username: myimdbuser
      password: mypass
      list: watchlist
    accept_all: yes
    queue_movies: yes
}}}

Or from RSS feed.

'''Example:'''

{{{
tasks:
  queue_from_foobar:
    rss: http://foobar.com/rss.xml # input
    accept_all: yes                # filter which accepts everything
    queue_movies: yes              # output entries to movie queue (with quality any)
}}}

These are not feeds in traditional !FlexGet sense as they don't download anything. Instead they are more like utility tasks.

Queue movies will work best with entries containing imdb_id/url or tmdb, if they're not available it will try to get them on it's own. Relying on this will mean that some of the entries may not be added to the [wiki:Plugins/movie_queue movie_queue].

== Options ==

You can also specify options for items being added to the movie queue. {{{quality}}} and {{{force}}} fields will be respected from entries, or they can be specified in the queue_movies config like so:

{{{
queue_movies:
  quality: 720p+ bluray
  force: no
}}}

See [wiki:Qualities qualities] page for valid quality requirements.