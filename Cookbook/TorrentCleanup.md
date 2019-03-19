# Torrent Cleanup Task

The clean_transmission plugin used to exist to remove old torrents from transmission after certain criteria had been met. This plugin was removed, but the behavior can now be replicated in a more flexible fashion. This recipe can also be adapted for deluge using the from_deluge and deluge plugins.

```yaml
tasks:
  remove stale torrents:
    from_transmission: yes
    disable: [seen, seen_info_hash]
    if:
      - transmission_progress == 100: accept
      - not transmission_seed_ratio_ok: reject
      - not transmission_idle_limit_ok: reject
    transmission:
      action: remove
```

### Defining Criteria
In order to determine what fields are available from the torrent client it is easiest to run a test like this:
```sh
flexget --test execute --tasks "remove stale torrents" --dump
```
The `--test` will ensure nothing is actually removed while you are testing, and the `--dump` means that all the available entry fields will be printed out. You can then determine which entry fields you would like to filter on.

### Plugins used:

- [from_transmission](/Plugins/from_transmission) This creates an entry for each torrent currently loaded in transmission. It provides entry fields prefixed with `transmission_` with information about the loaded torrent.
- [disable](/Plugins/disable) We disable seen plugins in this task since we want to consider every torrent loaded in transmission every time, no matter what has happened in other tasks or this task in the past.
- [if](/Plugins/if) We use the if plugin to accept only the entries we want to remove from transmission.
- [transmission](/Plugins/transmission) When the transmission plugin is used with the 'action' as remove, all accepted entries will be removed from transmission. The 'purge' action could be used instead to remove the torrent as well as the data from the drive.

### Transitioning from clean_transmission
Here is how you can emulate the old options for `clean_transmission` with this new system.

#### transmission_seed_limits
If you want to make sure the built in transmission seed limits (ratio and/or idle time) are respected, you can set the `only_complete` option for `from_transmission` plugin to `yes`. You can also check the `transmission_seed_ratio_ok` and/or `transmission_seed_ratio_ok` fields as shown in the example above.

```yaml
from_transmission:
  only_complete: yes
```

#### min_ratio
Replace the `3.0` in the following example with your desired minimum ratio.

```yaml
if:
  - transmission_ratio < 3.0: reject
```

#### finished_for
Replace the `days=3` with the amount of time you would like the torrent to be finished for.

```yaml
if:
  - transmission_date_done > now - timedelta(days=3): reject
```

#### delete_files
If you would like the files to be deleted as well, use the `purge` action with transmission plugin rather than `remove`.

```yaml
transmission:
  action: purge
```

#### tracker
If you only want to remove torrents from a given tracker.

```yaml
regexp:
  reject_excluding:
    - my_tracker:
        from: transmission_trackers
```
Or if you want to remove torrents from multiple trackers.
```yaml
regexp:
  reject_excluding:
    - tracker_a|tracker_b:
        from: transmission_trackers
```

#### preserve_tracker
If do not want to remove any torrents from a given tracker.

```yaml
regexp:
  reject:
    - my_tracker:
        from: transmission_trackers
```