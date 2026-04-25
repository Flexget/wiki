---
title: Anime Relations
description: Populate ID fields for different databases
published: false
date: 2026-04-25T01:10:26.352Z
tags: 
editor: markdown
dateCreated: 2026-04-25T01:10:26.352Z
---

# Anime Relations
Populates an entry with ID fields on different databases

```yaml
anime_relations: true
```
The plugin doesn't search for titles, only existing ID fields on the entry so at least one is required. It prioritizes the same order as the table below.
- If the source ID can match multiple results it will pick the most recent one.
  - When falling back to `tvdb_id` or `tmdb_id` it will try to use season information to narrow results down.


### Populated fields
| Field | Source | Searchable | Unique |
| --- | --- | --- | --- |
| `anidb_id` | [AniDB](/Plugins/anidb_list) | ✔ | ✔ |
| `al_id` | [AniList](/Plugins/anilist) | ✔ | ✔ |
| `mal_id` | [MyAnimeList](/Plugins/my_anime_list) | ✔ | ✔ |
| `animecountdown_id` | [Anime Countdown](https://animecountdown.com) | ✔ | ✔ |
| `ann_id` | [Anime News Network](https://www.animenewsnetwork.com) | ✔ | ✔ |
| `animeplanet_id` | [Anime Planet](https://anime-planet.com) | ✔ | ✔ |
| `anisearch_id` | [aniSearch](http://anisearch.com) | ✔ | ✔ |
| `imdb_id` | [IMDB](/Plugins/imdb_lookup) | ✔ | ❌ |
| `kitsu_id` | [Kitsu](/Plugins/kitsu) (Can be extracted from the plugin's `url` field) | ✔ | ✔ |
| `livechart_id` | [LiveChart](https://www.livechart.me) | ✔ | ✔ |
| `simkl_id` | [SIMKL](https://simkl.com) | ✔ | ✔ |
| `tmdb_id` | [TMDB](/Plugins/tmdb_lookup) | ✔ | ❌ |
| `tmdb_offset` | Episode offset in relation to AniDB. <br> For cases where TMDB merges seasons/cours into a single season | ❌ | ❌ |
| `tmdb_season` | TMDB season in relation to AniDB | ❌ | ❌ |
| `tvdb_id` | [TVDB](/Plugins/thetvdb_lookup) | ✔ | ❌ |
| `tvdb_offset` | Episode offset in relation to AniDB. <br> For cases where TVDB merges seasons/cours into a single season | ❌ | ❌ |
| `tvdb_season` | TVDB season in relation to AniDB | ❌ | ❌ |


## Example

```yaml
anime_relations: true
mock:
  - {title: 'Re:Zero kara Hajimeru Isekai Seikatsu 2nd Season', al_id: 108632}
accept_all: true
```
### Result:
```
─── Accepted ───────────────────────────────────────────────────────────────────────
title                      : Re:Zero kara Hajimeru Isekai Seikatsu 2nd Season
al_id                      : 108632
anidb_id                   : 14792
animecountdown_id          : 1063491
animeplanet_id             : re-zero-starting-life-in-another-world-season-2
anisearch_id               : 14302
ann_id                     : 22005
imdb_id                    : tt5607616
kitsu_id                   : 42198
livechart_id               : 9387
mal_id                     : 39587
simkl_id                   : 1063491
tmdb_id                    : 65942
tmdb_offset                : 26
tmdb_season                : 1
tvdb_id                    : 305089
tvdb_offset                : None
tvdb_season                : 2
```