= Discover =

Creates entries based on search results. Queries are produced by another input plugin.

=== Config Format ===
{{{
discover:
  what:
    - <input plugin config>
  from:
    - <search plugin>
  [limit]: <max results from each search engine>
  [type]: <normal|exact|movies>
}}}

'''Example:'''

This example would produce results from the torrentz search engine based on the movies currently in your [wiki:Plugins/movie_queue movie_queue].
{{{
discover:
  what:
    - emit_movie_queue: yes
  from:
    - torrentz
  type: movies
}}}