= Cleaning a Trakt List =
If you are using configure_series with a trakt list, periodically you may wish to remove shows which have ended. Nobody wants to do that manually, so here is a task to help.
{{{
trakt_list:
  username: ***
  password: ***
  api_key: ***
  custom: my list name
trakt_lookup: yes
if:
  - trakt_in_collection and trakt_series_status == 'Ended': accept
trakt_remove:
  username: ***
  password: ***
  api_key: ***
  list: my list name
}}}