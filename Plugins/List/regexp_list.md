---
title: regexp_list
description: 
published: true
date: 2022-12-12T10:00:01.508Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:14.773Z
---

# Regexp List
> This is part of [managed list](/Plugins/List) plugin system.
{.is-success}

It is a list of strings that represent regular expressions to be used for matching entries. The matching is case insensitive and only match single lines (no newline matching etc).

### Config
```yaml
regexp_list: <NAME>
```

### Usage
Maintain a list of regular expressions instead of writing them out in the config. Since it is a [list](/Plugins/List) plugin, you can use other list plugins to populate the regexp_list.

Below is an example that converts a list of series from a [trakt_list](/Plugins/List/trakt_list) to a list of regular expressions that can be used to match entries from RSS feeds. Useful if you don't care about series tracking.

```yaml
tasks:
  populate-regexp-list:
    disable: seen
    trakt_list:
      account: trakt_username
      list: my_shows
      type: shows
      strip_dates: yes
    list_add:
      - regexp_list: series_regexp
    manipulate:  # example: Pioneer One becomes pioneer.*one.*s\d{2}e\d{2}
      - title:
          replace:
            regexp: '$'
            format: ' s\d{2}e\d{2}'
      - title:
          replace:
            regexp: ' '
            format: '.*'
    accept_all: yes
    
  download-with-regexp:
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