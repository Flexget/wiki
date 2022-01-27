# Content size
Allow specifying minimum and maximum sizes for contents such as torrents and nzbs. By default the plugin operates in "strict" mode where if the size of a download cannot be determined it will be rejected.

**Note:** content_size doesn't work with magnet links, as it works by analyzing the the .torrent file. You can include the [magnets](/Plugins/magnets) plugin to reject any magnet entries.

### Example:
```
content_size:
  min: 12
  max: 1200
  strict: no
```

Size is given in MiB

This would reject all torrents below 12MiB and above 1200MiB and over rides the strict behaviour. Same would work also for nzbs. As this plugin only **Rejects**, you need to accept entries with some other filter (ie. [accept_all](/Plugins/accept_all), [series](/Plugins/series) etc.)