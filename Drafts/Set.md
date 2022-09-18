---
title: Set
description: 
published: true
date: 2022-09-18T04:58:28.848Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:58:26.273Z
---

# Set 2.0
```
set:
  [FIELD_NAME](/FIELD_NAME): <string format>

  [FIELD_NAME](/FIELD_NAME):
    {value]: <string format>
    [regexp](/regexp): <regexp groups>
    [replace](/replace): [<regexp what>, <with text>]
```

**Simple example:**

```
set:
  path: /foo/bar/%(series_name)s/
```


**Advanced example:**

```
set:
  path:
    value: /foo/bar/%(series_name)s/
    replace: [' ', '.']
```