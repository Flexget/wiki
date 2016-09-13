# Cleaning a Trakt List
If you are using configure_series with a trakt list, periodically you may wish to remove shows which have ended. Nobody wants to do that manually, so here is a task to help.
The `list_add` is optional, but maybe you want to move the show to an *Archive* list?
```
trakt_list:
  username: ***
  account: ***
  list: my list name
  type: shows
trakt_lookup: yes
accept_all: yes
disable: [ seen, input_cache ] #is necessary to not get cross-contamination effects with caching
if:
  - trakt_collected and trakt_series_status in ['ended', 'cancelled']: accept
list_add: #optional
  - trakt_list:
    username: ***
    account: ***
    list: another list
    type: shows
list_remove:
  - trakt_list:
    username: ***
    account: ***
    list: my list name
```