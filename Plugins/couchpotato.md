= Couchpotato =
This plugin creates an [wiki:Entry Entry] for each movie in your [https://couchpota.to/ couchpotato] wanted list.
This plugin can be used with the [wiki:Plugins/movie_queue movie_queue] plugin to add those movies to the queue.

== Plugin Settings ==

Currently the following settings are required:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''base_url'''||This is the url of your couchpotato instalation (usualy http://localhost) ||
||'''port'''||This is the port used by your couchpotato instalation (usualy 5050) ||
||'''api_key'''||This is api key of your couchpotato instalation (can be found under settings->general->advanced)  ||
}}}

=== Example: add movies to the movie queue ===
{{{
  queue_movies_couchpotato:
    couchpotato:
      base_url: http://localhost
      port: 5050
      api_key: <your key here>
    accept_all: yes
    movie_queue: add
}}}