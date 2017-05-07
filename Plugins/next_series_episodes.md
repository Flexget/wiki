# Next Series Episodes
Creates an [Entry](/Entry) for the next episode needed in each series you have configured in the [`series`](/Plugins/series) plugin (intended to be used with the [`discover`](/Plugins/discover) plugin). You must have one of either [`series`](/Plugins/series) or [`configure_series`](/Plugins/configure_series)  configured in the same task for this to work. 

If FlexGet has not seen the series for some time and is locked to specific episode numbering scheme, or if the series is not explicitly configured to some format via [`begin`](/Plugins/series/begin) or [`identified_by`](/Plugins/series/identified_by), `next_series_episodes` can not guess which episode to emit.

### Quality upgrades?
Once one quality has been successfully downloaded that episode is never created again. This means that ``discover`` with ``next_series_episodes`` does not currently work with quality upgrades.

### New series

If you would like to start every show automatically without setting the begin episode, you can configure ``next_series_episodes`` like this:

```yaml
next_series_episodes:
  from_start: yes
```
**NOTE**: This requires the [`series`](/Plugins/series) option [`identified_by`](/Plugins/series/identified_by) to be present and set to `ep`.

### Backfill

If you want flexget to attempt to retrieve any episodes you're missing from any season, you can configure `next_series_episodes` like this:

```yaml
next_series_episodes:
  backfill: yes
```

**NOTE**: Along with this setting, you must also set the [`series`](/Plugins/series)  option [`tracking`](/Plugins/series/tracking) to `backfill`, or `series` will reject the emitted episodes as being too far in the past.

### Examples

#### Manually specify begin in configuration

```yaml
discover:
  what:
    - next_series_episodes: yes
  from:
    - torrentz: verified
series:
  - my show:
      begin: S01E01
  - other show:
      begin: S03E01
```

#### Group configuration with backfill

```yaml
discover:
  what:
    - next_series_episodes:
        from_start: yes
        backfill: yes
  from:
    - torrentz: verified
series:
  settings:
    shows:
      identified_by: ep
      tracking: backfill
  shows:
    - my show
    - other show
```
