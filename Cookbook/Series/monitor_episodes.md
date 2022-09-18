---
title: monitor_episodes
description: 
published: true
date: 2022-09-18T05:21:52.701Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:50.178Z
---

This task will enable you to monitor and get notification for aired episodes that were not download using series plugin.

### Important notes:
The following example uses `series` plugin for simplicity's sake, but its most likely that this will be used with either an existing `template` calling `configure_series`. It is very important to add the `parse_only` attribute to the configuration, or FlexGet will assume that episodes were accepted.

```yaml
tasks:
  monitor_missing_episodes:
    seen: local # Use this so you won't affect other series tracking or get notified more than once per episode
    series: # Like I stated above, this is just a simple example
    - the flash (2014):
        parse_only: yes # This is very important, without this you will dirupt your tracking
    no_entries_ok: yes
    next_series_episodes: yes
    trakt_lookup: yes
    if:
    - trakt_ep_first_aired < now - timedelta(days=10): accept # Change the value in days to customize the time delta
    notify:
      task:
        title: "Missing episodes detected"
        message: |+
          {% for entry in task.entries %}
          An unreleased episode was detected: {{ entry.trakt_series_name }} - S{{ entry.trakt_season }}E{{ entry.trakt_episode|pad(2) }}
          Released on {{ entry.trakt_ep_first_aired|formatdate("%Y-%m-%d")}}
          {% endfor %}
        via:
        - pushover: 
            user_key: <user_key>
```