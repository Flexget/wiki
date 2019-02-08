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