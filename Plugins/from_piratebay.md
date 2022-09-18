---
title: from_piratebay
description: 
published: true
date: 2022-09-18T05:05:46.948Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:05:44.218Z
---

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

## Categories
|category | id|
|--|--|
|All| 0|
|Audio| 100|
|Music| 101|
|Audio books| 102|
|Sound clips| 103|
|FLAC| 104|
|Audio Other| 199|
|Video| 200|
|Movies| 201|
|Movies DVDR| 202|
|Music videos| 203|
|Movie clips| 204|
|TV shows| 205|
|Video Handheld| 206|
|HD - Movies| 207|
|HD - TV shows| 208|
|3D| 209|
|Video Other| 299|
|Applications| 300|
|App Windows| 301|
|App Mac| 302|
|App UNIX| 303|
|App Handheld| 304|
|App IOS (iPad/iPhone)| 305|
|App Android| 306|
|App Other OS| 399|
|Games| 400|
|Game PC| 401|
|Game Mac| 402|
|Game PSx| 403|
|Game XBOX360| 404|
|Game Wii| 405|
|Game Handheld| 406|
|Game IOS (iPad/iPhone)| 407|
|Game Android| 408|
|Game Other| 499|
|Porn| 500|
|Porn Movies| 501|
|Porn Movies DVDR| 502|
|Porn Pictures| 503|
|Porn Games| 504|
|Porn HD - Movies| 505|
|Porn Movie clips| 506|
|Porn Other| 599|
|Other| 600|
|E-books| 601|
|Comics| 602|
|Pictures| 603|
|Covers| 604|
|Physibles| 605|
|Other Other| 699|
