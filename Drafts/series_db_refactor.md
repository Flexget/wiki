# Allow controlling series settings from db
The idea is to adapt series plugin so that followed series (and all settings for them) can be controlled via the db (and thus via api) rather than just in the config.

## Stuff
- Replace (upgrade) internal series plugin [Series model](https://github.com/Flexget/Flexget/blob/develop/flexget/plugins/filter/series.py#L262) to include all the settings fields, similar to model in PR:1228, also have a default list, and named lists of series.

- Have a new configuration for the series filter plugin, which allows specifying one of the db series lists, rather than listing series directly in the config file.

- API/CLI etc. are then used to control the series and settings in the named series lists.

## Questions
The current Series db model gets updated from the config each time a task is run, so that things like series CLI work. How do we adapt that to new system? What named series list would the go in?

Is there a way to change settings for a whole db list? Or are they always stored per series?

configure_series, Does it write a list to db, or pass a text config to series plugin still?

## Suggestions
* All series will use a series list.
* If series is defined in config, it'll use a default reserved list name (`default_series_list` for example).
* Config specified series will reset list entirely, otherwise removing from list will be have to done manually.
* All tracking will be done internally in the list scope and not globally.
* `next_series_episodes` will be able to take a `series_list` name. By default it'll use the default series name.
* `configure_series` will still be used and will reset the default list. Behind the scenes it'll perform a list purge and then list add to the default list.
* Proposed ERD: ![erd](http://flexget.com/attachments/Drafts/series_db_refactor/series_erd.png)

## New Stuff

- Series matching using identifer( `tvdb_id`, `trakt_show_id`, etc.)
- Season pack support (?) *I'm not too sure that this should be bundled in with the whole refactor as it is a big deal of its own...*


### Attachments
* [draft 3](/attachments/Drafts/series_db_refactor/series_erd.png)