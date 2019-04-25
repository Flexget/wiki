# Kitsu

This plugin produces an [entry](/Entry) for each movie or series in a public [Kitsu.io](http://www.kitsu.io) library. Results are cached for two hours to avoid flooding the api.

**Notes:** 

 * Like with other APIs used by FlexGet the kitsu.io library is cached for 2 hours to avoid hammering.
 * You can find the **username** on their profile page or in the url. Only public entries in the libraries will be visible to this plugin.

## Configuration

| Option | Description |
| --- | --- |
| username | (required) Your or another user's kitsu.io username |
| lists | (required) list of libraries can contain `current`, `planned`, `completed`, `on_hold`, `dropped` |
| type | anime types can contain `ona`,`ova`,`tv`,`movie`,`music`,`special` |
| latest | If set to `yes` only the latest episode of the anime will be added as Entry (by appending the episode number to the end of the title) |
| status | can be `airing` or `finished`. Depends on the field `endDate` in the kitsu.io api which seems not always to be set or available at all. If it causes problems just remove this option |

## Examples

### Autoconfigure series

This example shows how the `kitsu` plugin could be used with the [configure_series](/Plugins/configure_series) plugin in order to download all of the anime you have added to your `current` and `planned` library.

```yaml
configure_series:
  from:
    kitsu:
      username: NikkyAi
      lists:
        - current
        - planned
      type:
        - ova
        - tv
  settings:
    identified_by: sequence
```

**Note:** using kitsu.io to match/accept entries in nyaa.se rss feeds works well (as long as the titles match more or less)