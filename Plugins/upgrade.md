# Upgrade
Upgrade plugin will continue getting better qualities of an entry (tracked by a unique identifier). It can also blocks any entry that are of a worse quality than you already have.

## Settings

| **Option** | **Description** |
| --- | --- |
| identified_by | Define how entries are identified, default `auto` which uses entry id field. Supports [Jinja Template](https://flexget.com/Jinja) |
| tracking | If enabled by it's self will track entry but not upgrade. |
| target | The target quality that should be upgraded to. Upgrades will not continue after target is met. |
| on_lower | action to preform. `allow` won't act on the entry (undecided) but allow it to by accepted by other plugins |
| timeframe | Allow upgrades for the given peroid of time |
| propers | Allow upgrade of same quality if proper is released |


## Syntax:

```
upgrade:
  identified_by: <template>
  tracking: [yes|no]
  target: <quality requirement>
  on_lower: [accept|reject|allow]
  timeframe: <interval>
  propers: [yes|no]
```

### Example for movies
In this example the first task will download movies based on imdb ratings. The second task will upgrade the movies already downloaded for 7 days.

```
tasks:
  high_rated_movies:
    upgrade:
      # We must add this so the upgrade plugin can track the downloaded qualities
      tracking: yes
    imdb_high_rated:
      imdb:
      min_score: 8.5
      min_votes: 5000

  upgrade_movies:
    upgrade:
      target: 1080p
      propers: yes
```

### Example for series

Series currently has the concept of upgrade. In the future series will be migrated to leverage this upgrade plugin.

In this example the first task will download epsiodes for existing series on the filesystem. The second task will upgrade any downloaded series.

```
tasks:
  existing_tv_shows:
    upgrade:
      # We must add this so the upgrade plugin can track the downloaded qualities
      tracking: yes
    configure_series:
      from:
        filesystem:
          - /media/series/

  upgrade_tv:
    upgrade:
      target: 1080p
      propers: yes
```

### Example with [timeframe](https://flexget.com/Plugins/timeframe)

In this example the first task will download epsiodes for existing series on the filesystem. It will wait for 720p for 6 hours if not accept what ever quality is available.

The second task will upgrade any downloaded series.

```
tasks:
  existing_tv_shows:
    upgrade:
      # We must add this so the upgrade plugin can track the downloaded qualities
      tracking: yes
    timeframe:
      wait: 6 hours
      target: 720p+
    configure_series:
      from:
        filesystem:
          - /media/series/

  upgrade_tv:
    upgrade:
      target: 1080p
      propers: yes
```



