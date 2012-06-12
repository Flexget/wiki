= All Series =

Automatically configures the [wiki:Plugins/series series] plugin for all series that appear in the feed.

Plugin expects the title format to start with the series name followed by the episode numbering. Use the [wiki:Plugins/manipulate manipulate] plugin to modify the entry title to match this format, if necessary. Since it's very hard to guess series names you're much more likely to get significantly more robust matching (and thus downloading) with configuring [wiki:Plugins/series series] plugin with '''explicit''' series names. You can also mix and match all different configuration methods.

'''Examples:'''

Turns on the plugin for a feed.

{{{
all_series: yes
}}}

== Series Settings ==

Behind the scenes, all_series just configures the [wiki:Plugins/series series] plugin with all the series it sees in the feed.''*'' You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin for all_series.

''' Example '''

{{{
all_series:
  path: /media/TV
  quality: 720p hdtv
  propers: no
}}}
