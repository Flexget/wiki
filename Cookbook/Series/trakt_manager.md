---
title: trakt_manager
description: 
published: true
date: 2022-09-18T05:25:34.631Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:22:05.600Z
---

# Manage your FlexGet series entirely from trakt.tv

This is a system designed for easily managing your FlexGet series from trakt.tv.

- You define shows you want to follow by creating a trakt list called `My TV Shows` (in this example, you can call it anything you want) and adding any shows you want the FlexGet series plugin to follow to that list.
- In order to make it easier to start getting a show from a certain episode, you can add the specific episode you want to start at to the `My TV Shows` list and it will be handled automatically.

```
templates:
  # This is just in a template so that it can easily be re-used in multiple tasks 
  # (for example in an rss based and discover based task)
  # If you only have one task using your series config, you can place
  # the configure_series plugin directly in that task rather than in a template
  tv:
    configure_series:
      settings:
        # Configure all the series options to your taste
        quality: 720p+
        path: /my/shows/{{series_name}}/Season {{series_season}}/  # This will sort your downloads if you are using one of the output plugins which supports it
        identified_by: ep
      from:
        trakt_list:
          account: myaccount
          list: My TV Shows
          type: shows
  
tasks:
  # This task will look for episodes you have added to your `My TV Shows` list at trakt.
  # It will set the `begin` series option for that show, then remove the episode and re-add 
  # it to your `My TV Shows` list as a show.
  follow-from-trakt:
    seen: local
    trakt_list:
      account: myaccount
      list: My TV Shows
      type: episodes
    accept_all: yes
    set_series_begin: yes
    list_remove:
      - trakt_list:
          account: myaccount
          list: My TV Shows
          type: episodes
    list_add:
      - trakt_list:
          account: myaccount
          list: My TV Shows
          type: shows

  # This task is what will actually download your shows.
  # See https://flexget.com/wiki/Cookbook/Series/Search 
  # for a more detailed explanation of how this search based task works,
  # as well as an example of how to use your `tv` template on an rss
  # based task alongside.
  discover-shows:
    # If this is your only task getting shows, you can just include 
    # the configure_series plugin here instead of using the template.
    template: tv
    discover:
      what:
        - next_series_episodes:
            from_start: yes
      from:
        - # Pick a search plugin(s) https://flexget.com/wiki/Searches
    # Add an appropriate output plugin here 
    # (perhaps `transmission` or `deluge` if you are using those clients.) 
    # https://flexget.com/wiki/Plugins#Output

# If you are using daemon mode, make sure you schedule the tasks in the right order, so
# that the begin episode gets set before it tries to download your shows
schedules:
  - tasks: [follow-from-trakt, discover-shows]
    interval:
      minutes: 30
```

Be sure to check the wiki pages for all the plugins used for more details:
- [configure_series](/Plugins/configure_series)
- [trakt_list](/Plugins/List/trakt_list)
- [discover](/Plugins/discover)
- [emit_series](/Plugins/emit_series)
- [set_series_begin](/Plugins/set_series_begin)
- [trakt_add](/Plugins/trakt_add)
- [trakt_remove](/Plugins/trakt_remove)
- [template](/Plugins/template)
- [scheduler](/Plugins/Daemon/scheduler)