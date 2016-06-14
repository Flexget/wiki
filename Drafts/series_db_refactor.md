= Allow controlling series settings from db =
The idea is to adapt series plugin so that followed series (and all settings for them) can be controlled via the db (and thus via api) rather than just in the config.

== Stuff ==
Replace (upgrade) internal series plugin [https://github.com/Flexget/Flexget/blob/develop/flexget/plugins/filter/series.py#L262 Series model] to include all the settings fields, similar to model in PR:1228, also have a default list, and named lists of series.

Have a new configuration for the series filter plugin, which allows specifying one of the db series lists, rather than listing series directly in the config file.

API/CLI etc. are then used to control the series and settings in the named series lists.

== Questions ==
The current Series db model gets updated from the config each time a task is run, so that things like series CLI work. How do we adapt that to new system? What named series list would the go in?

Is there a way to change settings for a whole db list? Or are they always stored per series?

configure_series, Does it write a list to db, or pass a text config to series plugin still?