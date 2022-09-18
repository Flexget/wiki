---
title: exists_series
description: 
published: true
date: 2022-09-18T05:05:01.065Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:04:58.504Z
---

# Existing series
This plugin will reject all entries that represent an episode of a series that is already on disk.

### Example

```yaml
exists_series: /storage/series/
```

### Example

```yaml
exists_series: 
  - /storage/series/
  - /downloads/series/
```

## Advanced

By default, the exists_series will not allow downloading of different qualities of the same episode. (If you already have Pioneer.One.S01E01.hdtv, Pioneer.One.S01E01.720p will be rejected.) If you would like to allow different qualities of the same episode, you can use the advanced form of configuration, like so:

```yaml
exists_series:
  path: /storage/series/
  allow_different_qualities: yes
```

If you would only like to allow qualities that are better than what is currently on disk, you can use this format:

```yaml
exists_series:
  path: /storage/series/
  allow_different_qualities: better
```

## Performance

If you have a large collection of series, this plugin can be slow to parse all of your files. If you have your episodes organized into folders, you can optimize the performance of the plugin by specifying the specific series folder with [Jinja](/Jinja):

```yaml
exists_series: '/storage/series/{{series_name}}'
```