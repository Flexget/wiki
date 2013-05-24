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
}}}

An overview of available search plugins can be found [wiki:Searches here].

For a list of installed search plugins run "flexget --search-plugins" from the cli

=== Example: Search movie queue ===

This example would produce results from the torrentz search engine based on the movies currently in your [wiki:Plugins/movie_queue movie_queue].

{{{
discover:
  what:
    - emit_movie_queue: yes
  from:
    - torrentz: verified
}}}
Be aware, that discover plugin just produces entries, if you want movies from your movie queue accepted you must still also include the [wiki:Plugins/movie_queue movie_queue] plugin in your task.