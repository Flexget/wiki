# Timeframe

Specify a timeframe in which FlexGet waits for the chosen quality. The desired quality should be given with `target` option, and should be a valid [quality requirements](/Qualities#Requirements) string. If specified quality does not become available within given `wait` after a different quality has been seen, best quality so far is chosen.

## Settings

| **Option** | **Description** |
| --- | --- |
| identified_by | Define how entries are identified, default `auto` which uses entry id [field](https://flexget.com/Entry). Supports [Jinja Template](https://flexget.com/Jinja) |
| target | The target quality that should be upgraded to. Upgrades will not continue after target is met. |
| wait | How long to wait for `target` quality. |
| on_waiting | The action to preform on entries which are pending for the `target` quality. `allow` won't act on the entry ([undecided](https://flexget.com/FilterOperations)). Default is `reject`
| on_reached | The action to preform on entries which reach the `target` quality or timeframe has expired. `allow` won't act on the entry ([undecided](https://flexget.com/FilterOperations)). Default is `accept`

## Syntax:

```
timeframe:
  identified_by: <jinja template>
  target: <quality requirement>
  wait: <NUM (minutes|hours|days|weeks)>
  on_waiting: [accept|reject|allow]
  on_reached: [accept|reject|allow]
```

### Example for movies
In this example the first task will download movies based on imdb ratings. It will wait for 720p-1080p for 1 day, if not fall back to best found.

```
tasks:
  high_rated_movies:
    timeframe:
      wait: 1 day
      # Let imdb handle the accept
      on_reached: allow
      target: 720p-1080p
    imdb_high_rated:
      imdb:
      min_score: 8.5
      min_votes: 5000
```

### Example for series

Series currently has the concept of timefeame. In the future series will be migrated to leverage this timeframe plugin.


```
tasks:
  existing_tv_shows:
    timeframe:
      wait: 1 day
      # Let series handle the accept
      on_reached: allow
      target: 720p-1080p
    configure_series:
      from:
        filesystem:
          - /media/series/
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

