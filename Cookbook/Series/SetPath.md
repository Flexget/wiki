= Set download path =

When using a bittorrent client plugin as your output plugin, ([wiki:Plugins/deluge deluge] or [wiki:Plugins/transmission transmission],) you can [wiki:Plugins/set set] the {{{path}}} field of an entry to control where the client will save the content (the set plugin is also available as a per series option). This, combined with [wiki:Plugins/set#DynamicFormatting jinja formatting] allows all series to be easily downloaded to separate series and season folders. This recipe uses the transmission plugin, but that can easily be replaced with the deluge plugin.

{{{
tasks:
  task-a:
    rss: http://example.com
    series:
      settings:
        seriesgroup:
          set:
            path: /series/location/{{series_name}}/Season {{series_season}}
      seriesgroup:    
        - Foo
        - Bar
        - CustomPathSeries:
            set:
              path: /series/location/CustomFolder/
    transmission: yes
}}}

Uses plugins: [wiki:Plugins/rss rss], [wiki:Plugins/series series], [wiki:Plugins/set set], [wiki:Plugins/transmission transmission]