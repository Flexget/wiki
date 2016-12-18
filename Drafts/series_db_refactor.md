# Allow controlling series settings from db
The idea is to adapt series plugin so that followed series (and all settings for them) can be controlled via the db (and thus via api) rather than just in the config.

## Stuff
- Replace (upgrade) internal series plugin [Series model](https://github.com/Flexget/Flexget/blob/develop/flexget/plugins/filter/series.py#L262) to include all the settings fields, similar to model in PR:1228, also have a default list, and named lists of series.

- Have a new configuration for the series filter plugin, which allows specifying one of the db series lists, rather than listing series directly in the config file.

- API/CLI etc. are then used to control the series and settings in the named series lists.

## Questions
The current Series db model gets updated from the config each time a task is run, so that things like series CLI work. How do we adapt that to new system? What named series list would the go in? <BR>
***Answer:*** A default series list will be updated via the config on each task run. We'll also seperate `series-tracking` capabilities and `series-list` ones via API/CLI.

Is there a way to change settings for a whole db list? Or are they always stored per series? <BR>
***Answer:*** Yes, `series_list` can be changed globally via API/CLI.

configure_series, Does it write a list to db, or pass a text config to series plugin still? <BR>
***Answer:*** Writes to `series_list` with a default name, does not deletes values from it, just marks relevant ones as `active` (similar to how we currently use `in_task`).

## Suggestions
* All series will use a series list.
* If series is defined in config, it'll use a default reserved list name (`default_series_list` for example).
* Config specified series will reset list entirely, otherwise removing from list will be have to done manually.
* All tracking will be done internally in the list scope and not globally.
* `next_series_episodes` will be able to take a `series_list` name. By default it'll use the default series name.
* `configure_series` will still be used and will reset the default list. Behind the scenes it'll add new values to list and mark them as `active`. All other values in the list will be marked as non active. Series filter will take only `active` series to consideration. 
* Proposed ERD: ![erd](https://flexget.com/attachments/Drafts/series_db_refactor/series_erd.png)

## New Stuff

- Series matching using identifer( `tvdb_id`, `trakt_show_id`, etc.)<BR>
- Season pack support ~~*I'm not too sure that this should be bundled in with the whole refactor as it is a big deal of its own...*~~ <BR>*Decided to delay this to a later time, too many changes at once.*


### Attachments
* [draft 3](/attachments/Drafts/series_db_refactor/series_erd.png)