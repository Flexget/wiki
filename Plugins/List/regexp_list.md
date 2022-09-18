---
title: regexp_list
description: 
published: true
date: 2022-09-18T05:25:34.631Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:14.773Z
---

# Regexp List
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

It is a list of strings that represent regular expressions to be used for matching entries. The matching is case insensitive and only match single lines (no newline matching etc).

### Config
```
regexp_list: <NAME>
```

### Usage
Maintain a list of regular expressions instead of writing them out in the config. Since it is a [list](/Plugins/List) plugin, you can use other list plugins to populate the regexp_list.

Below is an example that converts a list of series from a [trakt_list](/Plugins/List/trakt_list) to a list of regular expressions that can be used to match entries from RSS feeds. Useful if you don't care about series tracking.

```
populate_regexp_list:
    disable: seen
    trakt_list:
      account: trakt_username
      list: my_shows
      type: shows
      strip_dates: yes
    list_add:
      - regexp_list: series_regexp
    manipulate:  # example: Game of Thrones becomes game.*of.*thrones.*s\d{2}e\d{2}
      - title:
          replace:
            regexp: '$'
            format: ' s\d{2}e\d{2}'
      - title:
          replace:
            regexp: ' '
            format: '.*'
    accept_all: yes
  download_with_regexp:
    rss: https://some.url.com/rss
    list_match:
      from:
        - regexp_list: series_regexp
      remove_on_match: no
      single_match: no
    download: /some/download/path
```
### CLI
You can also [interact with regexp_list](/CLI/regexp-list) via command line.