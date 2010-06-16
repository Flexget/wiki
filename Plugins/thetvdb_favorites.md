= Thetvdb favorites =

This plugin will automatically configuring the [wiki:Plugins/series series] plugin with all the shows you have marked as favorites at [http://thetvdb.com].

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
