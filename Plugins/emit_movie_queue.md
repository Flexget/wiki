= Movie Queue Input =

Creates an [wiki:Entry Entry] for each movie in your [wiki:Plugins/movie_queue movie queue] (intended to be used with the [wiki:Plugins/discover discover] plugin).

=== Example ===

{{{
discover:
  what:
  - emit_movie_queue: yes
  from:
  - torrentz
  type: movies
movie_queue: yes
}}}

You should almost certainly use movie_queue: yes with this, like below.

{{{
movie_queue: yes
}}}

=== Notes ===

 * Somewhat poorly tested
 * Emits names in IMDB translated form, making this pretty useless with [wiki:Plugins/search search] if you live somewhere where english isn't primary language. A workaround for this problem is to make sure that you use the [wiki:Plugins/imdb_list imdb_list] plugin with username and password and then go to your imdb account and update your site preferences to "Title display country" as "United states" and "Title display language" as English.