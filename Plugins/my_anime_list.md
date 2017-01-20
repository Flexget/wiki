# MyAnimeList

This plugin produces an [entry](/Entry) for each item on [MyAnimeList](https://myanimelist.net) list. It can be used as a source for the [configure_series](/Plugins/configure_series) plugin.

**Notes:** 

 * Like with other APIs used by FlexGet the MyAnimeList is cached for 2 hours to avoid hammering.

 ## Configuration

| Option | Description |
| --- | --- |
| username | MAL username|
| status | MAL status used to filter entries, possible values: `watching`, `completed`, `on_hold`, `dropped` or `plan_to_watch`. Defaults to all. |
| type |Type of items to be listed, can be: `unknown`, `series`, `ova`, `movie`, `special`, `ona` or `music`. Defaults to all. |

## Examples
### Autoconfigure series
This example shows use of `my_anime_list` together with [configure_series](/Plugins/configure_series) to download all TV series user is planning to watch or currently watching.

```yaml
configure_series:
  from:
    my_anime_list:
      username: <<username>>
      status:
        - watching
        - plan_to_watch
      type: series
```
