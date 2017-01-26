# Path Selector
This plugin can be used to select a path based the disk usage.

### Configuration

| **Option** | **Description** |
| --- | --- |
| select | [most_free \| most_free_percent \| most_used \| most_used_percent] |
| paths | The paths to compare |
| within | Find other paths that are within size or percent. Default is 0 (disabled) |
| to_field | The entry field where to save the selected path. Default is path |

**NOTE:**

If you choose most_free_percent or most_used_percent then the within option must be set to 0-99%..

If you choose most_free or most_used then the within option should be set to 0-99SIZE.

Supported size format:


| Size in | Format | Example |
| --- | --- | --- |
| Megabytes | M, MiB, MB | 900MiB  |
| Gigabytes | G, GiB, GB | 10GiB  |
| Terabytes | T, TiB, TB | 1TiB  |

### Example (select path with most free space by percentage)
This example will find the path with the most free space by percent and any other paths that are within 2% difference. If it finds multiple paths then it will randomly select one.

If drive1 has 50%, drive2 has 52% and drive3 has 10% free then the plugin will randomly select drive1 or drive2.

```
tasks:
  TV:
    path_by_space:
      select: most_free_percent
      within: 2%
      paths:
        - /drive1/downloads/TV
        - /drive2/downloads/TV
        - /drive3/downloads/TV
```

### Example (select path with most free space by size)
This example will find the path with the most free space by size and any other paths that are within 5GiB difference. If it finds multiple paths then it will randomly select one.

If drive1 has 50GiB, drive2 has 20GiB and drive3 has 54GiB free then the plugin will randomly select drive1 or drive3.

```
tasks:
  TV:
    path_by_space:
      select: most_free
      within: 5GiB
      paths:
        - /drive1/downloads/TV
        - /drive2/downloads/TV
        - /drive3/downloads/TV
```