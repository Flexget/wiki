---
title: nyaa
description: 
published: true
date: 2022-12-07T05:18:51.818Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:18:17.084Z
---

# Nyaa
> This plugin is part of [search](/Plugins/Searches) plugin system
{.is-success}

Search plugin which gives results from [nyaa.si](http://nyaa.si/)
### Config
Takes two options:

**Category:**

Valid choices are `all`, `anime`, `anime eng`, `anime non-eng`, and `anime raw`

**Filter:**

Valid choices are `all`, `filter remakes`, `trusted only`, and `a+ only`

### Example

```yaml
nyaa:
  category: anime eng
  filter: trusted only
```