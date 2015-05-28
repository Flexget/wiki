= Couchpotato =
This plugin creates an [wiki:Entry Entry] for each movie in your [https://couchpota.to/ couchpotato] wanted list.
This plugin can be used with the [wiki:Plugins/movie_queue movie_queue] plugin to add those movies to the queue.

== Plugin Settings ==

Currently the following settings are required:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''base_url'''||This is the URL of your couchpotato installation (usually http://localhost) ||
||'''port'''||This is the port used by your couchpotato installation (usually 5050) ||
||'''api_key'''||This is API key of your couchpotato installation (can be found under settings->general->advanced)  ||
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