# Next Series Seasons

Creates an [Entry](/Entry) for the next season needed in each series you have configured in the [series](/Plugins/series) plugin (intended to be used with the [discover](/Plugins/discover) plugin). You must have either [series](/Plugins/series) or [configure_series](/Plugins/configure_series) plugin configured in the same task for this to work. 

If FlexGet has not seen the series for some time and locked to specific episode numbering scheme or if series is not explicitly configured to some format via `begin` or `identified_by` the `next_series_episodes` can not guess what to emit.

### Quality upgrades?
Once one quality has been successfully downloaded that season is never created again. This means that discover + `next_series_seasons` does not currently work with qualities upgrading.

### New series

If you would like to start every show automatically without setting the begin episode, you can configure `next_series_seasons` like this:

```yaml
next_series_seasons:
  from_start: yes
```
**NOTE**: This will require option [series](/Plugins/series) option `identified_by`, `begin` set to series or single call to `$ flexget series begin <name> <episode>`.  
It will also require configuring series to accept season packs via the [season_packs](/Plugins/series/season_packs) option.

### Backfill

Additionally, if you want flexget to attempt to retrieve any seasons you're missing from any season, you can configure `next_series_seasons` like this:

```yaml
next_series_seasons:
  backfill: yes
```

Note that with this setting, you must also set [series](/Plugins/series) plugin option `tracking` to backfill.

### Examples

#### Manually specify begin in configuration

```yaml
discover:
  what:
    - next_series_seasons: yes
  from:
    - torrentz: verified
series:
  - my show:
      begin: S01E01
      season_packs: yes
  - other show:
      begin: S03E01
      season_packs: yes
```

#### Group configuration with backfill

```yaml
discover:
  what:
    - next_series_seasons:
        from_start: yes
        backfill: yes
  from:
    - torrentz: verified
series:
  settings:
    shows:
      identified_by: ep
      tracking: backfill
      season_packs: yes
  shows:
    - my show
    - other show
```

Note that searching for season packs can obviouslly produce episodic results in the search site. If you're only intered in accpeting season packs, set `season_packs: only` in your series configuration. For more information see [season_packs](/Plugins/series/season_packs) wiki.