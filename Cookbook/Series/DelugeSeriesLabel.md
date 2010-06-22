= Deluge labels based on series name =
Deluge does not support spaces in label names, so this has to be worked around in order to have automatic labels based on series names. This can be accomplished by using the [wiki:Plugins/manipulate manipulate] plugin to create the label from series name with spaces replaced by underscores. We also need to use the [wiki:Plugins/plugin_priority plugin_priority] plugin to make the manipulate plugin run after the [wiki:Plugins/series series] plugin, so that the series plugin has a chance to populate the [wiki:Entry#Knownfields series_name field].
{{{
feeds:
  tv:
    rss: http://feed.com/feed
    series:
      - Series One
      - Series Two
    manipulate:
      label:
        from: series_name
        replace:
          regexp: ' '
          format: '_'
    plugin_priority:
      manipulate: 0
    deluge: yes
}}}