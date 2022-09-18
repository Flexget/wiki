---
title: --cli-config
description: 
published: true
date: 2022-09-18T05:00:45.321Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:00:42.751Z
---

# Commandline config
Allows specifying configuration values from commandline parameters.

Commandline values are specified in YAML by variable prefixed with dollar sign ($).
Commandline parameter must be comma separated list of variable=values.

Configuration example:

```
tasks:
  my task:
    rss: $url
    download: $path
```

Commandline example:

```
--cli-config "url=http://some.url/, path=~/downloads"
```