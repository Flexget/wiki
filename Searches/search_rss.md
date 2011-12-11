= Search_rss =

Many website allow the generation of rss feeds based on a query. This plugin takes advantage of this can generate rss feeds that contain the result of a query.

Take note that this plugin can not be used on the feed level and that it can only be used within [wiki:Plugins/discover discover] & [wiki:Plugins/urlrewrite_search urlrewrite_search] plugin.

== Config Format ==

All valid [wiki:Plugins/rss rss] plugin config options are valid here, just place {{{ {{search_term}} }}} into the url where the search term should go.

=== Simple configuration ===
{{{
search_rss: http://url{{<search_term>}}trailing url
}}}

=== Complex configuration ===

Search_rss supports all the advanced options from [wiki:Plugins/rss rss]

''' Example '''
{{{
search_rss:
  url: http://url{{<search_term>}}trailing url
  link:
    - link
    - magneturi
}}}

== Usage example ==

This example shows search_rss used within the [wiki:Plugins/discover discover] plugin. This particular example makes use of isohunt.com and generates an rss feed with the content of a search for each movie in the queue and generates entries from that rss feed. 
{{{
discover:
  what:
    - emit_movie_queue: yes
  from:
    - search_rss: http://isohunt.com/js/rss/{{search_term}}?iht=
}}}
For more information about the usage see this [wiki:Cookbook/Movies/discoverfeed recipe].
