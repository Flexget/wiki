= Trakt watched lookup =

Set the '''trakt_watched''' flag on all [wiki:Entry entries] about episodes you have marked seen in your [http://trakt.tv trakt.tv] account.

=== Example ===

{{{
  check_watched:
    find:
      path:
        - D:\Media\Incoming\series
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    trakt_watched:
      username: your_username
      password: your_password
      api_key: your_api_key
    if:
      - trakt_watched: accept
}}}