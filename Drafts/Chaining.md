---
title: Chaining
description: 
published: true
date: 2022-09-18T04:57:35.309Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:32.649Z
---

# Plugin chaining
Consider single tv preset for all series feeds ..

```
presets:
  tv:
    series_premieres: yes
    series:
      720p:
        - name
        - name
      hdtv:
        - name
        - name
```

You cannot really add quality to it since it will mess up series. You probably want to add some quality limitation to series_premieres though.

Currently you can workaround this by

```
presets:
  tv:
    series:
      720p:
        - name
        - name
      hdtv:
        - name
        - name
   premieres:
     series_premieres: yes
     quality: 
       min: hdtv
       max: 720p

```

however now you must make duplicate feeds, eg.

```
feeds:
  bitmetv:
    rss: ....
    preset: tv
  bitmetv-premieres:
    rss: .... (same as in bitmetv)
    presets: premieres
```

I don't know if this is a really a problem since inputs are cached, so the second hit to the same feed does not actually request anything.

But it might be cleaner if series_premieres were to allow specifying qualities.

```
series_premieres:
  quality:
    min: hdtv
    max: 720p
```

However re-implementing the quality into the series_premieres goes a bit against my practice. So it would make more sense to be able to utilize the existing quality plugin somehow.

## Plugin chaining
Make filtering API to plugins that works per entries. Example

```
def process(self, feed, entry):
  if 'foo' in entry[title](/title):
    feed.reject('bar')
```

Plugin could still use this when configure at feed level, eg.

```
def on_feed_filter(self, feed):
  for entry in feed.entries:
    self.process(feed, entry)
```

Register plugins with this API to new group (eg. chaining).

Allow configuring these plugins inside other plugins when appropriate.

Make some easy way to call all these from a plugin, maybe something similar to plugin_urlrewrite which provides urlrewrite framework.

### pros
 * we could potentially refactor almost all filtering plugins to this approach, would allow some very interesting combinations

### cons
 * this will cause confusion since previously chaining was not really possible (with the exception of set)
 * how deep does the chaining end up going? 


If this approach is taken, will we eventually end up with ugly yaml like

```
feeds:
  test:
    rss: .....
    regexp:
      - foo:
          imdb:
            min_score: 6.2
            quality:
              min: 720p
```

Now allowing stuff like this has been my plan in somewhere far far away (like version 3) WHEN we have a graphical interface for designing the filtering (see yahoo pipes, yes I had the same idea before I was aware of that service).