---
title: make_rss
description: 
published: true
date: 2022-09-18T05:07:52.808Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:50.210Z
---

# Output RSS

Write RSS containing succeeded (downloaded) entries.

#### Example
```yaml
make_rss: ~/public_html/flexget.rss
```

You may write into same file in multiple tasks.

#### Example
```yaml
my-task-A:
  make_rss: ~/public_html/series.rss
  .
  .
my-task-B:
  make_rss: ~/public_html/series.rss
  .
  .
```

With this example file `series.rss` would contain succeeded
entries from both tasks.

### Number of days / items
        
By default output contains items from last 7 days. You can specify
different perioid, number of items or both. Value -1 means unlimited.
        
#### Example
        
```
make_rss:
  file: ~/public_html/series.rss
  days: 2
  items: 10
```
          
Generate RSS that will containg last two days and no more than 10 items.
        
#### Example
```
make_rss:
  file: ~/public_html/series.rss
  days: -1
  items: 50
```
          
Generate RSS that will contain last 50 items, regardless of dates.
        
### RSS link
        
You can specify what [field](/Entry) from entry is used as a link in generated rss feed.
        
#### Example
```
make_rss:
  file: ~/public_html/series.rss
  link:
    - imdb_url
```
            
List should contain a list of [fields](/Entry) in order of preference.
Note that the url field is always used as last possible fallback
even without explicitly adding it into the list.
        
Default list: imdb_url, input_url, url

### Encoding
Since some clients do not support RSS properly (ahem, uTorrent). 

#### Example
```yaml
make_rss:
  file: ~/public_html/series.rss
  encoding: utf-8
```

## Templates
RSS plugin now supports templating the content and title. These can be achieved via following configuration.

*TODO: improve this section*

```yaml
make_rss:
  template: <file? or jinja2 template as inline>
  title: <jinja2 template>
```