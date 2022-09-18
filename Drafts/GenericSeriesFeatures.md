---
title: GenericSeriesFeatures
description: 
published: true
date: 2022-09-18T04:58:02.038Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:57:59.219Z
---

# Generic series features
**GOAL:** Extract nice functionalities like timeframe, quality upgrades etc into separate plugins that can be re-used with movies.

Each of these sub-functions should be separate plugin. Let's think timeframe for example.


```
class Timeframe:
  # plugin provides this service
  def evaluate(self, entry, identified_by, config):
      .
      .
      # return None or entry that should be accepted

  # can be used in task
  def on_task_filter(...):
      for e in entries:
          self.evaluate(....)
```


Example usage from series_plugin

```
accepted = plugin.get_plugin_by_name('timeframe').instance.evaluate(
    entry, "{0} {1}".format(series_name, series_id, timeframe_config)
```


Same approach would be used for all features. Some of the plugins would need to keep track of entries internally. Currently a backlog plugin is used to keep items in the task until timeframe for example does it's thing.

Ps. As an addition to timeframe I would like to set "deadline" for series, get something regardless of the quality before certain time.


### Plugins to do ?
	
```
timeframe:
  target: 720p
  amount: 12h
```  
 
```
deadline: 
 target: 720p
 amount: 12 hours
```

* Timeframe needs to operate on accepted entries in order to work well with other plugins

```
propers: 12 hours
```

```
qualities:
  - 720p
  - 1080p
```	

not so sure about this ....

```
upgrade:
  quality:
    - 720p
    - 1080p
  group:
    - FlexGet
    - Shit
```	

Using combination of these plugins might get a bit interesting ...


### Generic use in task
This could be used in task standalone

```
timeframe:
  identified_by: {{ series_name }} {{ series_id }}
  target: 720p
```


### Standalone with movies
```
rss: .....
imdb_lookup: yes
timeframe: 
  amount: 12h
  target: 720p
  identified_by: {{ imdb_id }}
imdb:
  min_score: 6.5
```
 
**NOTES:** 

* I hate how identified_by NEEDS to use jinja2 formatting, it makes no sense for enduser
(gazp) We could make this field be the inside of a jinja `{{}}` block (or even add the {{ magically only when the user didn't have them.) So you could write `imdb_id` or `series_name + series_id`

### With new movies plugin
```
rss: ....
movies:
  from:
    - movie_list: movies
  timeframe:
    amount: 12h
    target: 720p
```

**NOTES:** 

* movies plugin will need to supply identified_by to timeframe somehow
* does movies plugin bring anything here opposed to

```
rss: ...
imdb_lookup: yes
list_match:
  from:
    - movie_list: movies
timeframe:
  identified_by: {{ imdb_id }}
  amount: 12h
  target: 720p
```

## Identification mess
However specifying identified_by things manually suck .. but there is an alternative!

With movie_list we added ability to query id_field names from "movie_identifier" plugins. We need same done universally. All lookup plugins or any plugin that provides unique identifier should belong to group "identifiers" and have method to query the id field name.

So for `plugin.get_plugin_by_name('imdb').instance.identified_by()` would return `imdb_id`.

Series plugin is a bit problematic as it does not currently have unique identifier field, but it could have such field. Too bad we have already field `series_id` which is a bit different though :P

Usage with movies:

```
rss: ....
movies:
  from:
    - movie_list: movies
  info: imdb_lookup # applies to rss AND movies_list
  qualities: 
    - 720p
    - 1080p
```

Remember that plugin `movie_list` produced entries may contains id field(s) that were available at that time so those entries do not necessarily need to be looked up at all. Additionally we could make whole info field optional as we can detect what metainfo plugin was used for entries produced by `from`. Fall back to use normalized movie name if no identifier is found.


### Example flow (Quality)
Assuming we are using multiple ids and each id field is an identifier class. 

```
rss: .....
imdb_lookup: yes
tvdb_lookup: yes
regex:
  accept:
      - Game Of Thrones
quality:
  upgrade: true
  accept:
    - 720p hdtv
    - 1080p webdl
```
 
Identifers set by meta plugins

- Identifer(name='tvdb_id', value='123456')
- Identifer(name='imdb_id', value='123456')
- Identifer(name='series_id', value='S01E01', required=True) ... TODO: required?

First run (Game.Of.Thrones.S01E01.HDTV)
- Regex accepts
- Check if desired quality downloaded, NO (not desired quality) -> leave alone

Second run (Game.Of.Thrones.S01E01.720p)
- Regex accepts
- Check if desired quality downloaded, NO -> leave alone

Third run (Game.Of.Thrones.S01E01.720p)
- Regex accepts
- Check if desired quality downloaded, YES -> reject

Third run (Game.Of.Thrones.S01E01.1080p)
- Regex accepts
- Check if desired quality downloaded, NO -> leave alone

