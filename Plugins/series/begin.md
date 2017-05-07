# Begin
If you already have part of a show and need to specify where FlexGet should begin downloading, it can be done using the `begin` option. This should be equal to the first episode you want FlexGet to accept. This may not be needed in most cases, since FlexGet will not skip forward and back seasons due to [episode advancement](/Plugins/series/advancement) functionality. If you are using [``next_series_episodes``](/Plugins/next_series_episodes) or [``next_series_seasons``](/Plugins/next_series_seasons), those plugins will reference the `begin` episode if it's set. There are two ways to set this value: from config or from the CLI.

## Valid Values
The begin option can be set on series that are use 'ep', 'sequence', or 'date' `identified_by` mode. Setting the `begin` option will also set `identified_by` for the series, based on the format of the episode identifier used. Format for episode identifiers is as follows:

**ep:** SXXEYY, e.g. `S03E04`

**sequence:** Just the episode number, e.g. `13`

**date:** YYYY-MM-DD, e.g. `2013-03-04`

## Setting from CLI
To set `begin` for a show from the [CLI](https://flexget.com/CLI/series), use the `series begin` command:
```bash
flexget series begin "Name of Series" S02E01
```


## Setting from config
You can also set `begin` directly from a task config:

```
series:
  - Pioneer One:
      begin: S02E01
```

## Viewing
Setting `begin` via any of the methods above will save it in the database. You can see what the `begin` episode is for a given series by using the [CLI](https://flexget.com/CLI/series) command `series show`:
```
flexget series show "Show Name"
```

If a `begin` episode is set, it will be listed at the bottom of the resulting table. (Note it will also be reflected in the table, even if it hasn't been downloaded or seen, in which case all columns except the Entity ID will be empty.)

```yaml
┌My Show────┬────────────┬────────────────────────────────────┬──────────────────────┬────────┐
│ Entity ID │ Latest age │ Release titles                     │ Release Quality      │ Proper │
├───────────┼────────────┼────────────────────────────────────┼──────────────────────┼────────┤
│ S04E01    │            │                                    │                      │        │
└───────────┴────────────┴────────────────────────────────────┴──────────────────────┴────────┘
 * Downloaded

 Series uses `ep` mode to identify episode numbering (identified_by).
 See option `identified_by` for more information.
 Begin episode for this series set to `S04E01`.
 ```



## Removing

To remove the begin episode, use the [CLI](https://flexget.com/CLI/series) command `series forget` with the episode ID set as begin:
```bash
flexget series forget "My Show" S04E01