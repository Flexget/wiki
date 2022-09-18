---
title: pushbullet-complete-body
description: 
published: true
date: 2022-09-18T04:57:00.991Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:56:58.383Z
---

A more complete example of a configuration for pushbullet including more information from the series plugin. This of course can be expanded, but it is good to for figuring out how Jinja2 templates work. Also to test this try the mock task.

## Pushbullet configuration
```
templates:
  add_pushbullet:
    pushbullet:
      apikey: <API_KEY>
      title: "{{task}} - {% if series_name is defined %}\u0009{{series_name}}{% endif %} {% if ((series_episode is defined) and (series_episode is number)) %}{{ '%02d' % series_episode }}{% endif %}"
      body: "‣ episode:\u0009{% if tvdb_ep_name is defined %}{{tvdb_ep_name}}{% endif %}\r\n‣ season:\u0009\u0009{% if ((series_season is defined) and (series_season is number)) %}{{ '%02d' % series_season }}{% endif %}\r\n‣ air         date:\u0009\u0009{% if tvdb_ep_air_date is defined %}{{tvdb_ep_air_date.strftime('%d.%m.%Y')}}{% endif %}\r\n‣ proper:\u0009\u0009{% if proper is defined%}{% if proper %}yes{% else %}no{% endif %}{% endif %}"
```

Output in the format:
```
title: <Task name> - <Series Name> <Episode Number>
body:
  ‣ episode:   <episode name>
  ‣ season:    <season (0 prefix if less than 10)>
  ‣ air date:  <date (format: dd-mm-YY)>
  ‣ proper:    <true/false>
```

## Test
```
tasks:
  test_push:
    manual: true
    mock:
      - {title: 'Episode.Name.Goes.here.S01E02', url: 'https://www.google.com/289323', description: 'Some description here', proper: 'False', series_episode: '6', tvdb_ep_name: 'Some Episode Name', series_name: 'Series name', tvdb_ep_air_date: '2014-12-01 00:00:00', series_id: 'S01E02', series_episode: 6, series_season: 1}
    accept_all: yes
    seen: local
    disable: seen
    template:
      - add_pushbullet

via cli: flexget execute --task test_push
```
*Unfortunately the mock task does currently not support datetime hence you will receive an error when executing this test, remove the strftime function from the template and the test will run smoothly.*