---
title: metainfo_series
description: 
published: true
date: 2022-09-18T05:12:45.808Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:08:09.227Z
---

# Metainfo Series

Adds series metainfo fields to entries.

__```NOTE```__ This does not need to be used (and may cause problems) in a task if you are already using any of the series filtering plugins, ([series](/Plugins/series), [configure_series](/Plugins/configure_series), [all_series](/Plugins/all_series) or [series_premiere](/Plugins/series_premiere).) They already provide this information.

### Syntax

```yaml
metainfo_series: yes
```

This will add the following fields to an entry:

* id (eg: `Cool Series S01E01`)
* proper
* proper_count
* release_group
* series_episode
* series_episodes
* series_guessed
* series_id
* series_id_type
* series_name
* series_parser
* series_season

