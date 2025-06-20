---
title: Qualities
description: 
published: true
date: 2025-06-20T02:12:13.999Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:51:20.513Z
---

# Qualities
Qualities are split into five separate categories: resolution, source, codec, color range and audio. Any given release can have a value in all five of these categories. Here are all of the values within each category, listed with highest value at the top:

<!--
To update this table, you can run `flexget wiki-qualities` which will output the markdown to paste here.
-->

| Resolution | Source    | Codec | Color Range | Audio  |
|------------|-----------|-------|-------------|--------|
| 2160p      | bluray    | av1   | hybrid-hdr  | truehd |
| 1080p      | remux     | h265  | dolbyvision | dtshd  |
| 1080i      | dvdrip    | vp9   | hdrplus     | dts    |
| 720p       | webdl     | h264  | hdr         | flac   |
| 720i       | hdtv      | nvenc | 10bit       | dd+5.1 |
| hr         | webrip    | xvid  | 8bit        | ac3    |
| 576p       | bdscr     | divx  |             | dd5.1  |
| 540p       | dvdscr    |       |             | aac    |
| 480p       | sdtv      |       |             | mp3    |
| 368p       | dsr       |       |             |        |
| 360p       | tvrip     |       |             |        |
|            | preair    |       |             |        |
|            | ppvrip    |       |             |        |
|            | hdrip     |       |             |        |
|            | r5        |       |             |        |
|            | tc        |       |             |        |
|            | ts        |       |             |        |
|            | cam       |       |             |        |
|            | workprint |       |             |        |

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

> **NOTE:** Requirement strings that begin with a symbol need to be quoted, as in the above examples.
{.is-info}

### Common Requirements
There has been some confusion as to how to use this new system to specify some common release types, here are some examples.

**Standard HDTV Release**
  If you want to only download 'standard' HDTV releases, you also have to specify a resolution requirement, so that your filter does not include 720p HDTV releases as well: `hdtv <720p`

**720p Release**
  Just using `720p` as the requirement will work out well in most cases, but you may also want to also exclude things like preair releases. In this case you can make a minimum source requirement in addition to the resolution requirement: `720p hdtv+`