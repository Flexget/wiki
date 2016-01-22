= AniDB List =

This plugin produces an [wiki:Entry entry] for each movie on a public [http://www.anidb.net AniDB] wishlist. These entries can then be added to the [wiki:movie_queue#AddingRemovingusingTasks movie_queue], used to initiate a search with [wiki:discover discover], or passed to some other [wiki:Plugins#Outputs output plugin]. Results are cached for two hours to avoid flooding the site.
 
== Configuration ==

||=Option            =||==||=Description =||
||**user_id**         ||  ||Your or another user's AniDB id. ||


You can find the **user_id** on user's profile page. Their wishlist must be public.

== Usage notes ==

The plugin can easily be used to queue up films from your AniDB wishlist to be downloaded by another task:

{{{
anidb_list:
  user_id: anidbid
accept_all: yes
movie_queue: add
}}}
