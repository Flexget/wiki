# Timeframe

Specify a timeframe in which FlexGet waits for the chosen quality. The desired quality should be given with `target` option, and should be a valid [quality requirements](/Qualities#Requirements) string. If specified quality does not become available within given `wait` after a different quality has been seen, best quality so far is chosen.

## Settings

| **Option** | **Description** |
| --- | --- |
| identified_by | Define how entries are identified, default `auto` which uses entry id [field](https://flexget.com/Entry). Supports [Jinja Template](https://flexget.com/Jinja) |
| target | The target quality that should be upgraded to. Upgrades will not continue after target is met. |
| wait | How long to wait for `target` quality. |
| on_waiting | The action to preform on entries which are pending for the `target` quality. `allow` won't act on the entry ([undecided](https://flexget.com/FilterOperations)) 
| on_reached | action to preform. `allow` won't act on the entry (undecided) but allow it to by accepted by other plugins 

## Syntax:

```
upgrade:
  identified_by: <template>
  tracking: [yes|no]
  target: <quality requirement>
  on_lower: [accept|reject|allow]
  timeframe: <NUM (minutes|hours|days|weeks)>
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


### Example with [upgrade](https://flexget.com/Plugins/upgrade)

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

