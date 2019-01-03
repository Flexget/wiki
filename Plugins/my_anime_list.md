# MyAnimeList

This plugin produces an [entry](/Entry) for each item on [MyAnimeList](https://myanimelist.net) list. It can be used as a source for the [configure_series](/Plugins/configure_series) plugin.

**Notes:** 

 * Like with other APIs used by FlexGet the MyAnimeList is cached for 2 hours to avoid hammering.

 ## Configuration

| Option | Default | Description |
| --- | --- | --- | 
| username | | MAL username. _(Required)_ |
| status | _all_ | MAL status used to filter entries, possible values: `watching`, `completed`, `on_hold`, `dropped` or `plan_to_watch`. |
| airing\_status | _all_ | Airing status of the show used to filter entries, possible values: `airing`, `finished`, `planned` (also shown as _Not Yet Aired_ on MAL). |
| type | _all_ | Type of items to be listed, can be: `unknown`, `tv`, `ova`, `movie`, `special`, `ona` or `music`. |

## Examples
### Autoconfigure series
This example shows use of `my_anime_list` together with [configure_series](/Plugins/configure_series) to download all TV series user is planning to watch or currently watching, airing either now or in the future.

```yaml
configure_series:
  from:
    my_anime_list:
      username: <<username>>
      status:
        - watching
        - plan_to_watch
      airing_status:
        - airing
        - planned
      type: tv
```
