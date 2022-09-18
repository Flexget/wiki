---
title: set
description: 
published: true
date: 2022-09-18T05:15:25.520Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:12:49.699Z
---

# Set

Stores info in an [entry](/Entry). Can also do dynamic formatting per entry.

#### Example

```yaml
set:
  path: ~/torrents/
```

## Set as a sub-plugin

Certain plugins enable set commands to be called for a specific subset of entries from a task. Currently [regexp](/Plugins/regexp) and [series](/Plugins/series) support this format. The use of set in these cases is best understandable through examples.
 To set the stop ratio option for Some Show:

```yaml
series:
  - Some Show:
      set:
        ratio: 2.0
```
This example will set the label for this regexp, but not that regexp.

```yaml
regexp:
  accept:
    - this regexp:
        set:
          label: pizza
    - that regexp
```

## Plugins that accept Set keywords

Calling set however does not do much unless another plugin uses the information you have set. The following plugins (and likely more than listed here) will use values you have set with this plugin.

**[Deluge](/Plugins/deluge)**

 * `path`
 * `movedone`
 * `label`
 * `queuetotop`
 * `addpaused`
 * `maxupspeed`
 * `maxdownspeed`
 * `maxconnections`
 * `maxupslots`
 * `ratio`
 * `removeatratio`
 * `compact`
 * `automanaged`
 * `content_filename`

**[Transmission](/Plugins/transmission)**

 * `path`
 * `content_filename`
 * `addpaused`
 * `maxconnections`
 * `maxupspeed`
 * `maxdownspeed`
 * `ratio`

**[Download](/Plugins/download)**

 * `path`
 * `filename`

Options configured from the set plugin will override configuration values set directly in the plugin that is reading them.
