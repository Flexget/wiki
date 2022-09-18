---
title: next-episode
description: 
published: true
date: 2022-09-18T05:21:56.552Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:21:53.927Z
---

# Use next-episode.net as input for import_series
This feed will pull your series from [http://next-episode.net](http://next-episode.net) using [import_series](/Plugins/import_series)
There are some transmission stuff included in the example to. 

First you need to set up your account at http://next-episode.net and select your series. Then you need to locate the iCal-url, it's located under calender: Export to iCal File. It will look like this: http://next-episode.net/PAGES/misc/export_calendar?z&u=user&k=<numbers>.ics

```
templates:
  tv:
    transmission:
      host: localhost
      port: 9091
      username: user
      password: password
      ratio: 1
      removewhendone: yes
    exists_series:
      - /home/public/TV/
    import_series:
      settings:
        quality: webdl|hdtv <=720p
        target: 720p
        timeframe: 36 hours
        set:
          path: /home/public/TV/{{series_name}}/Season {{"%02d"|format(series_season)}}
      from:
        text:
          url: (url to ical)
          entry: 
            title: ^SUMMARY:(.*) - [0-9](/0-9)+x[0-9](/0-9)+.*$
            url: ^SUMMARY:(.*) - [0-9](/0-9)+x[0-9](/0-9)+.*$
    download:
      path: /home/torrent
      overwrite: yes
      fail_html: no

feeds:
  my-feed-a:
    rss: hdtvrss
    template: tv 
  my-feed-b:
    rss: sdtvrss 
    template: tv 

```