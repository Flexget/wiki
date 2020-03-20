# AniList

This plugin produces an [entry](/Entry) for each item on a user's [AniList](https://anilist.co) list. It can be used as a source for the [configure_series](/Plugins/configure_series) plugin.

**Notes:** 

 * Like with other APIs used by FlexGet, the AniList is cached for 2 hours to avoid hammering.

 ## Configuration

| Option | Description | Default | Possible Values |
| --- | --- | --- | --- |
| username | _(Required)_ AniList username. | | 
| status | Your defined status on AniList. | `current`, `planning` | `current`, `planning`, `completed`, `dropped`, `paused`, `repeating` |
| release\_status | Airing status of the show. | `all` | `releasing`, `finished`, `not_yet_released`, `cancelled` |
| format | Type of items to be listed. | `all` | `tv`, `tv_short`, `ova`, `movie`, `special`, `ona` |
| list | Filter by user's [custom anime lists](https://anilist.co/settings/lists).<br>Supports multiple entries | | Custom list title (case-sensitive)|

## Output
Will try to populate the following fields for its entries:
| Field | Description |
| --- | --- |
| `al_banner` | Banner image |
| `al_cover` | Cover image |
| `al_episodes` | Episode count |
| `al_format` | Media format (same as the `format` setting above) |
| `al_genres` | |
| `al_idMal` | ID on MyAnimeList |
| `al_links` | Official links from AniList. eg: The show's official site and streaming services |
| `al_list` | List title |
| `al_list_status` | Populated by default lists, custom lists will return empty. |
| `al_release_status`| Airing status (same as the `release_status` setting above) |
| `al_tags` | |
| `al_title` | Dictionary with show titles in Romaji and English (if available) |
| `al_trailer` | URL to trailer embed (YouTube or Dailymotion) |
| `alternate_name` | Show's alternate titles. Automatically includes English |
| `title` | Romaji title |

## Examples
### Add to list
This example adds a user's `anilist` entries using all the default values to a custom [entry-list](/Plugins/List/entry_list) for further processing by other tasks.
```yaml
anilist: <<username>>
list_add:
  - entry-list: anilist-entries
```
### Autoconfigure series
This example shows use of `anilist` together with [configure_series](/Plugins/configure_series) to download episodes of anime the user is currently watching and is airing either now or in the future.

```yaml
configure_series:
  settings:
    identified_by: sequence
  from:
    anilist:
      username: <<username>>
      status: current
      release_status:
        - releasing
        - not_yet_released
      format:
        - tv
        - tv_short
```

This will only configure shows the user added to their [AniList custom anime lists](https://anilist.co/settings/lists) named `Winter Seasonals` and `Spring Seasonals`
```yaml
configure_series:
  settings:
    identified_by: sequence
  from:
    anilist:
      username: <<username>>
      status: all
      list:
        - Winter Seasonals
        - Spring Seasonals
```