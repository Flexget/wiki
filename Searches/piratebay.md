# Pirate Bay
This search plugin will get results from [http://thepiratebay.se](/http://thepiratebay.se)

## Configuration
Simplest configuration, uses default search options. (all categories, sort by seeders)
```
piratebay: yes
```
Advanced usage:

| Option | Description |
| --- | --- |
| category | One of: all, audio, music, video, tv, movies, highres movies, highres tv, comics. You can also directly specify the category number from thepiratebay if the category you need is not directly supported. |
| sort_by | One of: date, size, seeds, leechers, default (note that this is the piratebay default search order, flexget sorts by seeds by default) |
| sort_reverse | `yes` or `no`. |
**Example:**
```
piratebay:
  category: video
  sort_by: leechers
```