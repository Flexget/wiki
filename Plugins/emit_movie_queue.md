= Movie Queue Input =
'''IMPORTANT: `movie_queue` plugin is set for deprecation and will be replaced with [wiki:Plugins/movie_list movie_list].

Creates an [wiki:Entry Entry] for each movie in your [wiki:Plugins/movie_queue movie queue] (intended to be used with the [wiki:Plugins/discover discover] plugin).

=== Example ===

{{{
discover:
  what:
  - emit_movie_queue: yes
  from:
  - torrentz: verified
movie_queue: accept
}}}

You should almost certainly use movie_queue: yes with this, like below.

{{{
movie_queue: yes
}}}

=== Queue names ===

If movies were added to [wiki:Plugins/movie_queue movie queue] using a queue name, you emit from that queue by using `queue_name`:
{{{
discover:
  what:
  - emit_movie_queue:
      queue_name: a queue name
  from:
  - torrentz: verified
movie_queue: accept
}}}

=== Notes ===

 * `queue_name` is case insensitive
 * Emits names in IMDB translated form, making this pretty useless with [wiki:Plugins/search search] if you live somewhere where english isn't primary language. A workaround for this problem is to make sure that you use the [wiki:Plugins/imdb_list imdb_list] plugin with username and password and then go to your imdb account and update your site preferences to "Title display country" as "United states" and "Title display language" as English.