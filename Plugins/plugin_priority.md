---
title: plugin_priority
description: 
published: true
date: 2022-09-18T05:13:17.002Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:49.884Z
---

# Plugin priority
Each plugin has default priority which usually makes the most sense, however in some cases you may want to run particular plugin before another. With priority plugin you can change default priority values in a task. Higher values are execute first. You can use `flexget plugins` to view default priorities. Note that this works only within [phases](/Plugins/sleep). Meaning you can not move plugin from output phase to work at input phase.
        
**Example:**

```
plugin_priority:
  series: 240
  manipulate: 250
```