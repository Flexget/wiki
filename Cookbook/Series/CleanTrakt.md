# Cleaning a Trakt List
If you are using configure_series with a trakt list, periodically you may wish to remove shows which have ended. Nobody wants to do that manually, so here is a task to help.
```
trakt_list:
  username: ***
  password: ***
  list: my list name
  type: shows
trakt_lookup: yes
if:
  - trakt_in_collection and trakt_series_status == 'ended': accept
if:
  - trakt_in_collection and trakt_series_status == 'canceled': accept
trakt_remove:
  username: ***
  password: ***
  list: my list name
```