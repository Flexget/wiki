---
title: CLISearch
description: 
published: true
date: 2022-09-18T04:55:06.207Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:55:03.600Z
---

This example is missing an output, but it was designed to use Deluge since movedone and content_filename are included.
This task was created to do two things:
1. Grab / Start a folder for a series
2. Catch up a Series if episodes where missing.

Because manual: yes is set this task will not run normally you will have to call it directly, and that is needed because it depends on the --cli-config so it has something to search for

To run the task you would do one of the following note that the season number is optional but useful since the rss feed will only return so many results, --disable-advancement is used since exists_series will be used to prevent dup episodes:

```
flexget --test execute --tasks SearchEZTV --cli-config "show=[Yourshowname],season=[number]" --disable-advancement
flexget --test execute --tasks SearchEZTV --cli-config "show=[Yourshowname]" --disable-advancement
```


```
SearchEZTV:
    discover:
      what:
        - mock: 
          - title: $show
      from:
        - search_rss: http://www.ezrss.it/search/index.php?show_name={{search_term}}&season=$season&show_name_exact=false&quality=hdtv&mode=rss
      type: any
    thetvdb_lookup: yes
    exists_series:
      - /TV/$show
    series:
      settings:
        hdtv:
          set:
            movedone: '/TV/{{series_name}}/Season {{series_season}}'
            content_filename: "{{ series_name }} - {{ series_id }} - {{ ep_name|default('Unknown') }}  - {{ quality|upper }}"
      hdtv:
        - $show
    manual: yes
```

Notes:

mock is normally used for testing with a hard coded value, but since we need a way to pass a value to discover it works here.

$show and $season are replaced by the values passed from the --cli-config plugin
