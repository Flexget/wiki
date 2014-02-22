= Check subtitles =

Set the '''subtitles''' field on all [wiki:Entry entries] about local files found having subtitles. The field is a list of available languages.

=== Example ===

{{{
  check_subs:
    find:
      path:
        - D:\Media\Incoming\series
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    check_subtitles: yes
    if:
      - "subtitles and 'ita' in subtitles": accept
}}}