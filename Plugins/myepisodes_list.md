= !MyEpisodes list =

This plugin creates an [wiki:Entry Entry] for each show in your [http://www.myepisodes.com myepisodes.com] show list.

This plugin is useful for example when used to control the series plugin using [wiki:Plugins/configure_series configure_series].[[BR]]

== Plugin Settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''username'''||This is your username at [http://www.myepisodes.com myepisodes.com] ||
||'''password'''||Your [http://www.myepisodes.com myepisodes.com] password. ||
||'''strip_dates'''||If set to {{{yes}}}, the year will be removed from the end of titles that contain them.||
||'''include_ignored'''||If set to {{{yes}}}, shows you've put on ignore will be included as well.||
}}}

== Config format ==

{{{
myepisodes_list:
  username: <value>
  password: <value>
  strip_dates: <yes|no>
  include_ignored: <yes|no>
}}}

=== Example: Autoconfigure series ===

This example shows how the trakt_list plugin could be used with the [wiki:Plugins/configure_series configure_series] plugin in order to download all of the series you have included in a custom trakt list called 'following shows'.

{{{
configure_series:
  from:
    myepisodes_list:
      username: myepisodesusername
      password: myepodoespassword
  settings:
    quality: 720p
}}}


== Related plugins ==
* You can use the [[Plugins/myepisodes|myepisodes]] plugin for marking accepted entries as 'Acquired'.