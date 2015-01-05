= Discover =

Creates entries based on search results. Queries are produced based on another input plugin(s).

== Config Format ==

{{{
discover:
  what:
    - <input plugin config>
  from:
    - <search plugin>
  [limit]: <max results from each search engine>
  [interval]: <time between trying each search again>
  [ignore_estimations]: <if yes, no release date checking is tried>
}}}

An overview of available search plugins can be found [wiki:Searches here]. For a list of installed search plugins run "flexget --search-plugins" (`flexget plugins --group search` on Flexget>=1.2) from the cli.

=== Example: Input configs ===

It's advised to have inputs queued to series or movies list (via for example a task doing '[wiki:Plugins/queue_movies queue_movies]: yes'). Then use either:

{{{
discover:
      what:
        - emit_series: yes
        # OR
        - emit_movie_queue: yes
      from:
        ...
}}}

It's also possible to have inputs directly looked up here (but not advised as it would look up each time and not appear in your queues):

{{{
discover:
      what:
        - imdb_list:
            list: watchlist
        - trakt_list:
            username: USERNAME
            password: PASSWORD
            list: watchlist
            type: movies
      from:
        ...
}}}

=== Example: Search movie queue ===

This example would produce results from the torrentz search engine based on the movies currently in your [wiki:Plugins/movie_queue movie_queue].

{{{
discover:
  what:
    - emit_movie_queue: yes
  from:
    - kat:
        category: movies
        verified: yes
    - piratebay:
        category: "highres movies"
        sort_by: seeds
    - torrentz: verified
  interval: 1 day
}}}
Be aware, that discover plugin just produces entries, if you want movies from your movie queue accepted you must still also include the [wiki:Plugins/movie_queue movie_queue] plugin in your task.