= Thetvdb favorites =

This plugin will automatically configuring the [wiki:Plugins/series series] plugin with all the shows you have marked as favorites at [http://thetvdb.com]. If thetvdb goes down, the last known list of favorites will be used until it comes back online.

You configure thetvdb_favorites plugin with your account id at thetvdb. You can find it on the [http://thetvdb.com/?tab=userinfo account tab] after you log in.

''' Example '''

{{{
thetvdb_favorites:
  account_id: 320D93B3A1
}}}

== Series Settings ==

Behind the scenes, thetvdb_favorites just configures the [wiki:Plugins/series series] plugin with all your favorites from thetvdb. You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin for your thetvdb shows.

''' Example '''

{{{
thetvdb_favorites:
  account_id: 320D93B3A1
  timeframe: 12 hours
  quality: 720p
  propers: 3 days
}}}
