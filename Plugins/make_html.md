---
title: make_html
description: 
published: true
date: 2022-09-18T05:07:48.984Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:07:46.475Z
---

# Make HTML
Generate an HTML file for accepted entries.

## Options

| **Name** | **Info** | **Description** |
| --- | --- | --- |
|  file  |  Text  |  File to be created  |
|  template  |  Text  |  Specify a custom Jinja template. Custom templates should be placed in <flexget config dir>/templates/. Defaults to builtin template (html.template).  |

**Example:**

```yaml
make_html:
  file: ~/thefile.html
```

## Using templated

Custom templates should (typically) be placed in 
`~/.flexget/templates`

This directory is not created for you. If you are using an alternate config location then you should update the path accordingly.