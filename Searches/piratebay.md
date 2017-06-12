# Pirate Bay
This search plugin will get results from [http://thepiratebay.se](/http://thepiratebay.se)

## Configuration
Simplest configuration, uses default search options. (all categories, sort by seeders)
```
piratebay: yes
```
If you would like to define a custom category, or sort options you can use the following options:

- category: *all, audio, music, video, tv, movies, highres movies, highres tv, comics*. You can also directly specify the category number from thepiratebay if the category you need is not directly supported.
- sort_by: *date, size, seeds, leechers, default (note that this is the piratebay default search order, flexget sorts by seeds by default)*
- sort_reverse: Can be yes or no.

**Example:**
```
piratebay:
  category: video
  sort_by: leechers
```