= Search for Episodes =

This recipe will cause !FlexGet to search for the next episode you need for any of your configured series rather than wait for it to appear in a rss feed for example.

The [wiki:Plugins/discover discover] plugin will act as an input just like [wiki:Plugins/rss rss] plugin would. It does intelligent searches from listed [wiki:Searches search] plugins. The content it tries to find comes from the configured [wiki:Plugins/emit_series emit_series] plugin. The emit_series plugin will output the next episodes from all of your series configured in the task, even if they come from preset or via some other manner.

If !FlexGet does not already have a history of a given show, the [wiki:Plugins/series/begin begin] option or `--series-begin` must be used for the series in order for emit_series to start working. In this example we set begin to be S01E01 for every show in our series config, so that !FlexGet will start looking for the episodes starting at the first one.

{{{ #!python
presets:
  tv:
    series:
      settings:
        my group:
          quality: 720p
          begin: S01E01
      my group:
        - my show
        - my other show

tasks:
  # classic rss feed monitoring
  monitor feed:
    rss: http://example.com
    preset: [tv]

  # new shiny automatic searching
  search series:
    preset: [tv]
    discover:
      what:
        - emit_series: yes
      from:
        - torrentz: verified
      interval: 1 hour  # Search for expected episodes again every hour
}}}

This snippet does not include an [wiki:Plugins#Outputs output] plugin. You will need to add the appropriate one to the task when implementing this recipe.