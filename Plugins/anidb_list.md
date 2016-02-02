= AniDB List =

This plugin produces an [wiki:Entry entry] for each movie or series on a public [http://www.anidb.net AniDB] wishlist. These entries can then be added to the [wiki:movie_queue#AddingRemovingusingTasks movie_queue], used to initiate a search with [wiki:discover discover], or passed to some other [wiki:Plugins#Outputs output plugin]. Results are cached for two hours to avoid flooding the site.

'''Notes:''' 

 * Like with other APIs used by !FlexGet the AniDB list is cached for 2 hours to avoid hammering.
 * Adding this plugin to your movie tasks or preset will NOT cause movies or series in the trakt list to be accepted since this is an input, not a filter.
 * You can find the **user_id** on their profile page. Their wishlist must be public.

== Configuration ==

{{{#!div style="margin-left: 25px"
||=Option            =||=Description =||
||**user_id**         ||Your or another user's AniDB id. ||
||'''type'''          ||Type of items to be listed, can be one of: `movies` or `shows`
||'''strip_dates'''   ||If set to {{{yes}}} the year will be removed from the end of titles that contain them.||


== Usage notes ==

The plugin can easily be used to queue up films from your AniDB wishlist to be downloaded by another task:

{{{
anidb_list:
  user_id: anidbid
accept_all: yes
movie_queue: add
}}}

=== Example: Autoconfigure series ===

This example shows how the anidb_list plugin could be used with the [wiki:Plugins/configure_series configure_series] plugin in order to download all of the series you have included in your wishlist.

{{{
configure_series:
  from:
    anidb_list:
      user_id: anidbid
      type: shows
  settings:
    quality: 720p
}}}