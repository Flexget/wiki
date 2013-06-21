= Search for Episodes =

This recipe will cause !FlexGet to search for the next episode you need for any of your configured series rather than wait for it appear in a different input plugin.

The [wiki:Plugins/emit_series emit_series] plugin is used within the [wiki:Plugins/discover discover] plugin in order to achieve this effect. The emit_series plugin will create an entry representing the next episode you need for each of the series configured in the series plugin. The discover plugin will then search for that episode using any of the [wiki:Searches search] plugins you have configured. The series plugin will then accept the found episodes in the normal manner.

If !FlexGet does not already have a history of a given show, the [wiki:Plugins/series/begin begin] option must be specified for the series in order for emit_series to start working. In this example we set begin to be S01E01 for every show in our series config, so that !FlexGet will start looking for the episodes starting at the first one.

{{{ #!python
tasks:
  search series:
    series:
      settings:
        my group:
          quality: 720p
          begin: S01E01
      my group:
        - my show
        - my other show
    discover:
      what:
        - emit_series: yes
      from:
        - torrentz: verified
      interval: 1 hour  # Search for expected episodes again every hour
}}}

This snippet does not include an [wiki:Plugins#Outputs output] plugin. You will need to add the appropriate one to the task when implementing this recipe.