# from_piratebay
Generate entries based on www.thepiratebay.org listings, filtered by categories and ranks.

## Configuration
Simplest configuration, get entries from `HD - Movies` category using default options (default mirror, top torrents, all ranks).
```yaml
from_piratebay:
  category: HD - Movies
```
Advanced usage:

| Option | Description |
| --- | --- |
| category | One of category name (case-sensitive) from Categories, or a category ID number such as `207` for `HD - Movies`. |
| url | URL (including the protocol) to a valid piratebay API mirror, such as `http://piratebayztemzmv.onion`. Default is `https://apibay.org`. |
| list | One of `top`, `top48h`, `recent`. Default is `top`, the list of most popular torrents. `top48h` is the list of most popular torrents during the last 48 hours. |
| rank | One of `all`, `member`, `vip`, `trusted`, `supermod` from low to high. Selecting a lower rank will include torrents from higher ranks. Default is `all`. |
**Example:**
```yaml
from_piratebay:
  url: https://apibay.org
  category: HD - Movies
  list: top
  rank: all
```