---
title: Qualities
description: 
published: true
date: 2022-09-21T21:25:07.640Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:20.513Z
---

# Qualities
Qualities are split into five separate categories: resolution, source, codec, color range and audio. Any given release can have a value in all five of these categories. Here are all of the values within each category, listed with highest value at the top:

|Resolution|Source|Codec|Color Range|Audio|
|---|---|---|---|---|
|2160p<br>1080p<br>1080i<br>720p<br>720i<br>hr<br>576p<br>540p<br>480p<br>368p<br>360p|bluray<br>remux<br>dvdrip<br>webdl<br>hdtv<br>webrip<br>bdscr<br>dvdscr<br>sdtv<br>dsr<br>tvrip<br>preair<br>ppvrip<br>hdrip<br>r5<br>tc<br>ts<br>cam<br>workprint|h265<br>vp9<br>h264<br>xvid<br>divx|dolbyvision<br>hdrplus<br>hdr<br>10bit<br>8bit|truehd<br>dtshd<br>dts<br>flac<br>dd+5.1<br>ac3<br>dd5.1<br>aac<br>mp3|

## Requirements
In your config, you are not limited to specifying a single quality you want, you can specify individual values, or ranges, in all five categories. Any category you do not specify in your requirements implies that any value is ok for that category.

**Ranges:**
To specify a range in a given category, write the lower and upper bound, with a dash in between. Note that a range must be between two items of the same category (in the same column above.) Examples:
```
720p-1080p
hdtv-bluray
```

**Open ended range:**
If you would just like to specify a lower bound on the category, you can follow it with a plus. Examples:
```
480p+
tvrip+
```
If you would like to place just an upper bound, this is also possible with the <= symbol.
```
<=720p
<=bluray
```

**Discrete values:**
If you would like to specify one value, multiple acceptable values for a category, but nothing inbetween them, you can use a pipe to join them. The pipe essentially means 'or'. Examples:
```
720p
sdtv|hdtv
dd5.1|dts|aac
```

**Disallowing values:**
If you just want to block certain values from being acceptable, you can prefix them with an exclamation mark. Examples:
```
!dts
!cam
!10bit
```

### Putting it together
So, any time a quality (range) needs to be specified in the config, you can combine these techniques to define the acceptable values for each category. If your quality string starts with a symbol, instead of a letter or number, you have to place quotes around the whole thing. Here are some examples of complete quality requirements that could be used in your config:

```
hdtv
720p
720p hdtv+
360p-720p hdtv divx|xvid
360p !dts
"!h264 !dts"
"<=720p"
```

**NOTE:** Requirement strings that begin with a symbol need to be quoted, as in the above examples.

### Common Requirements
There has been some confusion as to how to use this new system to specify some common release types, here are some examples.

**Standard HDTV Release**
  If you want to only download 'standard' HDTV releases, you also have to specify a resolution requirement, so that your filter does not include 720p HDTV releases as well: `hdtv <720p`

**720p Release**
  Just using `720p` as the requirement will work out well in most cases, but you may also want to also exclude things like preair releases. In this case you can make a minimum source requirement in addition to the resolution requirement: `720p hdtv+`