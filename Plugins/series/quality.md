## Quality

| **Name** | **Description** |
| --- | --- |
| quality | Accept only qualities that match this quality requirement. No other quality will be accepted. |
| qualities | Accept all given qualities, multiple downloads |

Values should all be specified as a valid [quality requirement](/Qualities#Requirements) string.

**Example:**

```
series:
  - name of series 1:
      quality: 720p+
  - name of series 2:
      qualities:
        - pdtv !h264
        - 720p hdtv|webdl
```

Usually best way to specify quality for series is to use groups:

**Example:**

```
series:
  720p:
    - name of series 1
    - name of series 2
  hdtv:
    - name of series 3
    - name of series 4
```

See [groups](/Plugins/series/per_group_settings) for more information.