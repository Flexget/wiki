= Series Premiere =
Accepts any entry that appears to be the first episode of a series.''*''

'''Examples:'''

Turns on the plugin for a feed.
{{{
series_premiere: yes
}}}
You can also override the path for all entries that series_premiere accepts.
{{{
series_premiere: ~/TV/Premieres
}}}

''*'''''NOTE:''' this plugin only looks in the entry title and expects the title format to start with the series name followed by the episode info. Use the [wiki:Plugins/manipulate manipulate] plugin to modify the entry title to match this format, if necessary.