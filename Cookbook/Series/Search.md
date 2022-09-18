---
title: Search
description: 
published: true
date: 2022-09-18T05:27:32.249Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:59.634Z
---

# Search for Episodes
This recipe will cause FlexGet to search for the next episode you need for any of your configured series rather than wait for it to appear in a rss feed for example.

The [discover](/Plugins/discover) plugin will act as an input just like [rss](/Plugins/rss) plugin would. It does intelligent searches from listed [search](/Searches) plugins. The content it tries to find comes from the configured [next_series_episodes](/Plugins/next_series_episodes) plugin. The next_series_episodes plugin will output the next episodes from all of your series configured in the task, even if they come from a template or via some other manner.

If FlexGet does not already have a history of a given show, normally the [begin](/Plugins/series/begin) option or `series begin` command must be used for the series in order for [next_series_episodes](/Plugins/next_series_episodes) to start working. In this example we set the `from_start` option of [next_series_episodes](/Plugins/next_series_episodes) so that FlexGet will start looking for the episodes of all shows starting at the first one.

```yaml
templates:
  tv:
    series:
      settings:
        my group:
          quality: 720p
      my group:
        - my show
        - my other show

tasks:
  # classic rss feed monitoring
  monitor-feed:
    rss: http://example.com
    template: [tv]

  # automatic searching
  discover-series:
    template: [tv]
    discover:
      what:
        - next_series_episodes:
            from_start: yes
      from:
        - torrentz: verified
      interval: 1 hour  # Search for expected episodes again every hour
```

This snippet does not include an [output](/Plugins#Outputs) plugin. You will need to add the appropriate one to the task when implementing this recipe.