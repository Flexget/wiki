# Next Series Seasons

Creates an [Entry](/Entry) for the next season needed in each series you have configured in the [`series`](/Plugins/series) plugin (intended to be used with the [`discover`](/Plugins/discover) plugin). You must have one of either [`series`](/Plugins/series) or [`configure_series`](/Plugins/configure_series)  configured in the same task for this to work. 

If FlexGet has not seen the series for some time and is locked to specific episode numbering scheme, or if the series is not explicitly configured to some format via [`begin`](/Plugins/series/begin) or [`identified_by`](/Plugins/series/identified_by), `next_series_seasons` can not guess which season to emit.

Note that searching for season packs can produce episode results, depending on the search site. If you only want to accept season packs, set `season_packs: only` in your series configuration. For more information see the `series` [`season_packs`](/Plugins/series/season_packs) option.

### Quality upgrades
Once one quality has been successfully downloaded that episode is never created again. This means that ``discover`` with ``next_series_seasons`` does not currently work with quality upgrades.

### New series

If you would like to start every show automatically without setting the begin episode, you can configure `next_series_seasons` like this:

```yaml
next_series_seasons:
  from_start: yes
```
**NOTE**: This requires the [`series`](/Plugins/series) option [`identified_by`](/Plugins/series/identified_by) to be present and set to `ep`.

### Backfill

If you want flexget to attempt to retrieve any episodes you're missing from any season, you can configure `next_series_seasons` like this:

```yaml
next_series_seasons:
  backfill: yes
```

**NOTE**: Along with this setting, you must also set the [`series`](/Plugins/series)  option [`tracking`](/Plugins/series/tracking) to `backfill`, or `series` will reject the emitted seasons as being too far in the past.

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