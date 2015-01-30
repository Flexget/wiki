This task will search the paths you select for series related files in an effort to fill in gaps in your series tracking database.

This is useful if your feeds break and you have downloaded a bunch of series files or if you want to populate the series tracking database quickly after resetting it.

{{{
  Sync_Series:
    manual: yes
    find:
      path:
        - /[path to your series folders]/
      regexp: '.*\.(mp4|avi|mkv)$'
      recursive: yes
    disable: builtins
    all_series:
      tracking: no
    exec: echo "Found {{title}}"
}}}
