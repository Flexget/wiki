---
title: new_qualities
description: 
published: true
date: 2022-09-18T04:58:55.814Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:53.084Z
---

# Qualities
Qualities are split into four separate categories: resolution, source, codec, and audio. Any given release can have a value in all four of these categories. Here are all of the values within each category, listed with highest value at the top:

```th
** Resolutions **
```
```th
** Sources **
```
```th
** Codecs **
```
```th
** Audio **
```
|--------
```td style="vertical-align: top"
- 1080p
- 1080i
- 720p
- 720i
- hr
- 576p
- 480p
- 368p
- 360p
```
```td style="vertical-align: top"
- bluray
- dvdrip
- webdl
- hdtv
- bdscr
- dvdscr
- webrip
- sdtv
- dsr
- tvrip
- preair
- ppvrip
- !r5
- tc
- ts
- cam
- workprint
```
```td style="vertical-align: top"
- 10bit
- h264
- xvid
- divx
```
```td style="vertical-align: top"
- dts
- ac3
- aac
- dd5.1
- mp3
```

## Requirements
In your config, you are not limited to specifying a single quality you want, you can specify individual values, or ranges, in all four categories. Any category you do not specify in your requirements implies that any value is ok for that category.

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
If you would like to specify one value, multiple acceptable values for a category, but nothing inbetween them, you can use a pipe to join them. Examples:
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
So, any time a quality range needs to be specified in the config, you can combine these techniques to define the acceptable values for each category. If your quality string starts with a symbol, instead of a letter or number, you have to place quotes around the whole thing. Here are some examples of complete quality requirements that could be used in your config:
```
hdtv
720p
720p hdtv+
360p-720p hdtv divx|xvid
360p !dts
"!h264 !dts"
"<=720p"
```

## Series Plugin Changes
The `min_quality` and `max_qaulity` options have been removed. These are replaced by the normal `quality` option, as it now supports ranges directly. The other major change is to the `timeframe` feature. Instead of defining your desired quality with the `quality` option, you define it in the new option `enough`. Your `quality` setting will continue to be respected, even after the timeframe has expired.

Here is an example config change that would be required.
Old way:
```
series:
  settings:
    groupa:
      quality: 720p
      timeframe: 6 hours
      min_quality: hdtv
      max_quality: 720p
```
New way:
```
series:
  settings:
    groupa:
      enough: 720p
      timeframe: 6 hours
      quality: hdtv+ <=720p
```

## Quality Plugin Changes
`min` and `max` options have been removed, ranges can be specified without them now.
Config, old way:
```
quality:
  min: 720p
  max: 1080p
```
New way: (You probably want to add the a source requirement, like dsr+ bit here so that you don't get 'cam' or 'workprint' etc. sources)
```
quality: 720p-1080p dsr+
```

## Movie Queue Plugin (and Queue Movies) Changes
When adding a movie to the queue, either via CLI or through queue_movies plugin, you can now specify quality in the new manner.

Examples:
```
flexget --movie-queue add "A Good Movie" "720p+ bluray+"
```
```
queue_movies:
  quality: 720p-1080p bluray
```