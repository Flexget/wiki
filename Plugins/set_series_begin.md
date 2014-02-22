= Set series begin =

This plugin sets the episode to start getting a series from, for each accepted entry with '''series_name''' (tv show title) and '''series_id''' (episode id, like S01E03) fields.

=== Example ===

{{{
  series_begin:
    trakt_emit:
      username: your_username
      password: your_password
      api_key: your_api_key
      context: collected
    accept_all: yes
    set_series_begin: yes
}}}