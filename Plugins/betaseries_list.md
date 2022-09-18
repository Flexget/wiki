---
title: betaseries_list
description: 
published: true
date: 2022-09-18T05:02:56.550Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:33.572Z
---

# betaseries list
This plugin creates an [Entry](/Entry) for each serie a betaseries member follows.

This plugin is useful for when used in a task with the [configure_series](/Plugins/configure_series) plugin to add series from your betaseries watchlist.

**Notes:** 

 * Like with other APIs used by FlexGet the betaseries list is cached for 2 hours to avoid hammering.

**Example:**

```
configure_series:
  from:
    betaseries_list:
      username: xxxxx
      password: xxxxx
      api_key: xxxxx
```

You Api key can be requested freely at http://www.betaseries.com/api.

**Example:**

If you want to download the series followed by multiple members

```
configure_series:
  from:
    betaseries_list:
      username: xxxxx
      password: xxxxx
      api_key: xxxxx
      members:
        - some_name
        - another_guy            
```
