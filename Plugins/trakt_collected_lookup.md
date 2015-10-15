= Trakt collected lookup =

Set the '''trakt_in_collection''' flag on all [wiki:Entry entries] about episodes you have marked collected in your [http://trakt.tv trakt.tv] account.

=== Example ===

{{{
  check_collected:
    filesystem:
      path:
        - D:\Media\Incoming\series
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    trakt_collected_lookup:
      username: your_username
      password: your_password
      api_key: your_api_key
    if:
      - trakt_in_collection: accept
}}}