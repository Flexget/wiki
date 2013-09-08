= Series Premiere =
Accepts any entry that appears to be the first episode of a series.''*''

'''Examples:'''

Turns on the plugin for a task.
{{{
series_premiere: yes
}}}

== Series Settings ==

Behind the scenes, series_premieres just configures the [wiki:Plugins/series series] plugin with all the premieres it sees in the task.''*'' You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin for series_premire.

There are two options specific to series_premiere also available:

 `allow_teasers`::
   By default, S01E00 episodes will also be accepted, to turn this off, set this to `no`
 `allow_seasonless`::
   If you would also like to get initial episodes of series which do not have a season, (e.g. 'Mini.Series.Episode.I.hdtv',) you can set this to `yes`

''' Example '''

{{{
series_premiere:
  path: /media/TV/Premieres
  quality: hdtv <=720p
  propers: no
  allow_teasers: no
}}}

''*'''''NOTE:''' this plugin only looks in the entry title and expects the title format to start with the series name followed by the episode info. Use the [wiki:Plugins/manipulate manipulate] plugin to modify the entry title to match this format, if necessary.