= Thetvdb favorites =

This plugin will automatically configuring the [wiki:Plugins/series series] plugin with all the shows you have marked as favorites at [http://thetvdb.com]. If thetvdb goes down, the last known list of favorites will be used until it comes back online.

You configure thetvdb_favorites plugin with your account id at thetvdb. You can find it on the [http://thetvdb.com/?tab=userinfo account tab] after you log in.
=== Example ===

{{{
thetvdb_favorites:
  account_id: 320D93B3A1
}}}

=== Advanced Example ===

Behind the scenes, thetvdb_favorites just merges your list of favorites into the series plugin under a [wiki:Plugins/series#Groupsettings series group] called thetvdb_favs. If you would like to use the advanced options of the series plugin, you can do so using a configuration like this:

{{{
thetvdb_favorites:
  account_id: 320D93B3A1
series:
  settings:
    thetvdb_favs:
      timeframe: 12 hours
      quality: 720p
      propers: 3 days
}}}

You can also override the series group that thetvdb_favorites places your favorites into like this:
{{{
thetvdb_favorites:
  account_id: 320D93B3A1
  series_group: my_group_name
}}}
