---
title: text
description: 
published: true
date: 2022-09-18T05:14:06.297Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:14:03.752Z
---

# Text
Parse any text for entries using regular expression. This doesn't work well with HTML, please use [html](/Plugins/html) instead.

```
text:
  url: <url>
  entry:
    <field>: <regexp to match value>
  format:
    <field>: <python string formatting>
  encoding: <encoding of file (defaults to utf-8)>
```

Format can be used to modify matched values. All fields that were parsed are usable. You can also make temp fields for data if you need.

**Note:** each entry must have at least two fields, title and url.

### Example:
```
text:
  url: http://www.nbc.com/Heroes/js/novels.js
  # construct our entry with this data
  entry:
    title: novelTitle = "(.*)"
    url: novelPrint = "(.*)"
  # further format entry
  format:
    url: http://www.nbc.com%(url)s
```