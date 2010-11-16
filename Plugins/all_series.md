= All Series =
Accepts any entry that appears to be an episode of a series.''*''

'''Examples:'''

Turns on the plugin for a feed.
{{{
all_series: yes
}}}

== Series Settings ==

Behind the scenes, series_premieres just configures the [wiki:Plugins/series series] plugin with all the series it sees in the feed.''*'' You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin for series_premire.

''' Example '''

{{{
all_series:
  path: /media/TV
  min_quality: hdtv
  max_quality: 720p
  propers: no
}}}

''*'''''NOTE:''' this plugin only looks in the entry title and expects the title format to start with the series name followed by the episode info. Use the [wiki:Plugins/manipulate manipulate] plugin to modify the entry title to match this format, if necessary.