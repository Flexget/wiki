= From Uoccin =
This plugin creates an [wiki:Entry Entry] for each series or movies you have added to your watchlist in [https://play.google.com/store/apps/details?id=net.ggelardi.uoccin Uoccin], and can be used in combination with [wiki:Plugins/configure_series configure_series] or [wiki:Plugins/discover discover] to search for episodes or movies to download.

'''{{{NOTE:}}}''' you need to set up a task to let Flexget synchronize the local uoccin.json file with the Android app (see [wiki:uoccin_reader uoccin_reader]).[[BR]]

== Plugin Settings ==

Currently the following settings are supported:

{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''path'''||This is the path to the uoccin.json file.||
||'''type'''||What kind of entries you want the plugin to produce: can be '''movies''', '''series''' or '''episode'''.||
||'''tags'''||(Optional) One or more tags to filter the entries.||
||'''check_tags'''||(Optional) How do you want to filter by tags: can be '''any''' (default, it means the movies or series marked with one or more of the specified tags will be included), '''all''' (only movies or series marked with *all* the specified tags will be included) or '''none''' (only movies or series *not* marked with any of the specified tags will be included).||
||'''ep_flags'''||(Optional) What kind of episodes you want to include in the list: can be '''watched''' (default) or '''collected'''.||
}}}

=== Example: series ===

This example shows how the from_uoccin plugin could be used with the [wiki:Plugins/configure_series configure_series] plugin.

{{{
  get_series:
    sequence:
      - configure_series:
          settings:
            quality: 720p hdtv+
          from:
            from_uoccin :
              path: path_to_uoccin_folder
              type: series
              tags: [ 'hires' ]
      - configure_series:
          settings:
            quality: webrip
          from:
            from_uoccin :
              path: path_to_uoccin_folder
              type: series
              tags: [ 'netflix' ]
}}}
[[BR]]

=== Example: movies ===

This example shows how the from_uoccin plugin could be used with the [wiki:Plugins/discover discover] plugin.

{{{
  get_movies:
    discover:
      what:
        - from_uoccin :
            path: path_to_uoccin_folder
            type: movies
      from:
        - torrentz: verified
}}}

[[BR]]
