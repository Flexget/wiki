# Remove gaps in your series database by searching a folder for episodes you already downloaded

This task will search the paths you select for series related files in an effort to fill in gaps in your series tracking database.

This is useful if your feeds break and you have downloaded a bunch of series files or if you want to populate the series tracking database quickly after resetting it.

```
sync-series:
    manual: yes
    filesystem:
      path:
        - /[path to your series folders]/
      regexp: '.*\.(mp4|avi|mkv)$'
      recursive: yes
    disable: builtins
    configure_series:
      settings:
        set:
          tracking: no
      from:
        filesystem:
          - /[path to your series folders]/

    exec: echo "Found {{title}}"
```

Your folder names need to be very clear and clean "Subfolder should be series names".. 

To run this task, use: flexget execute --task sync-series