= Series Premiere =
Accepts any entry that appears to be the first episode of a series.''*''

'''Examples:'''

Turns on the plugin for a feed.
{{{
series_premiere: yes
}}}

== Series Settings ==

Behind the scenes, series_premieres just configures the [wiki:Plugins/series series] plugin with all the premieres it sees in the feed.''*'' You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin for series_premire.

''' Example '''

{{{
series_premiere:
  path: /media/TV/Premieres
  quality: hdtv <=720p
  propers: no
}}}

''*'''''NOTE:''' this plugin only looks in the entry title and expects the title format to start with the series name followed by the episode info. Use the [wiki:Plugins/manipulate manipulate] plugin to modify the entry title to match this format, if necessary.