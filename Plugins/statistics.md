---
title: statistics
description: 
published: true
date: 2022-09-18T05:15:33.210Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:13:32.517Z
---

# Output Statistics
**UNMAINTAINED - WORKS POORLY. Dropped in r1238**


Output graphs about downloaded entries. The output is a single HTML file with graphs linked from Google chart API.

**Example:**

```
global:
   statistics: 
      file: ~/public_html/flexget_stats/index.html
```

# Output Statistics 2.0
The old statistics plugin is crap, no one maintains it, and it really doesn't log anything useful. Since FlexGet 1.x has a fancy sqlite database, we can use that to get better statistics in addition to analyzing entries on output.

The next question is the drawing method, [Google charts](http://code.google.com/apis/chart/) (the current system) or [flot](http://code.google.com/p/flot/)?

## Database
### What can we get?
* Number of episodes downloaded for each serie
* Quality for downloads (HDTV, 720p, etc..)
* Group names?

### What do we WANT but can't?
* Download history for [Plugins/deluge](/Plugins/deluge) and [Plugins/transmissionrpc](/Plugins/transmissionrpc)

## Entries
### What can we get?
* IMDB score (average score for downloaded movies?)
* Torrent size downloaded (min, max, average, average per feed)

### What do we WANT but can't?