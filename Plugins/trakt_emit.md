= Trakt emit =

'''{{{IMPORTANT:}}} Please see [wiki:Plugins/trakt trakt] on how to authorize Flexget to access your private Trakt.tv account.'''

'''{{{WARNING:}}}''' There is currently a problem with this plugin where it will not emit the next episode properly for a season when it has not yet been aired. #2831

This plugin creates an [wiki:Entry Entry] for the next episode to watch or to collect for each show you have marked seen or collected in your [http://trakt.tv trakt.tv] account.

This plugin can be used in combination with several plugins, like [wiki:Plugins/discover discover] to search for new episodes to download, or [wiki:Plugins/set_series_begin set_series_begin] to reset the first episode for configured series, and so on.[[BR]]

== Plugin Settings ==

Currently the following settings are supported:


||='''Option'''=||='''Description'''=||
||'''username'''||This is your username at [http://trakt.tv trakt.tv] ||
||'''account'''||Your account name set by [wiki:Plugins/trakt Trakt] cli tools. '''Required''' if the list is private.||
||'''context'''||Can be '''watched''' (default) or '''collected''', it refers to the seen and collected [http://trakt.tv trakt.tv] status.||
||'''position'''||Can be '''next''' (default) or '''last''', combined to the "context" option, instructs the plugin to emit the next to watch, the next to collect, the last watched or the last collected episode for each series.||
||'''list'''||The name of a custom [http://trakt.tv trakt.tv] or built-in list to limit the series for which to emit entries.||
||'''strip_dates'''||If set to {{{yes}}} the year will be removed from the end of titles that contain them.||


=== Example: set series begin ===

This example shows how the trakt_emit plugin could be used with the [wiki:Plugins/set_series_begin set_series_begin] plugin in order to set the first episode to download for the series in the my_tv_show list on [http://trakt.tv trakt.tv]. By default !FlexGet will start from first episode it sees in the task. This is mainly useful if you set up discover.

{{{
tasks:
  sync-trakt:
    trakt_emit:
      username: your_username
      account: your_account
      context: collected
      list: my_tv_show
    accept_all: yes
    set_series_begin: yes
}}}

[[BR]]
'''Notes:'''

[http://trakt.tv trakt.tv] will not emit any info for series the user has never marked seen or collected, even if the '''list''' option is used and the actual custom list contains them. However, when this situation occurs, the plugin will emit a default S01E01 episode id, but only with the '''list''' option and '''position'''='''next'''.