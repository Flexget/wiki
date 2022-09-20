---
title: Imports
description: 
published: true
date: 2022-09-20T05:12:20.187Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:19:14.943Z
---

# Wiki `import`

## Using Import
Wiki.js currently does not have an official way to import content, but we have a workaround with javascript. Putting a link to another wiki page, followed by `{.include}` to mark it with the include class will cause the link to be replaced with the contents of that page. 

```markdown
[Anything you want here](/Path/To/OtherPage){.include}
```

If you are adding something that will be used on multiple pages, please add it in the [Includes](/Includes/) directory. Click the Index button on that page (at the top-left next to "FLEXGET") to view existing files.

## Plugin information

> These kinds of imports with variable filling do not currently work on our new wiki software (wiki.js)!
{.is-danger}

### Requires additional libraries via pip
```yaml
---
import:
 - Includes/PluginRequiresPip
packages: a b c
---

[Includes/PluginRequiresPip](/Includes/PluginRequiresPip){.include}
```

## Info

```yaml
---
import:
 - Includes/PluginInfo
info: text here
---

[Includes/PluginInfo](/Includes/PluginInfo){.include}

```

## Replaced and Removed Plugins
#### Plugin Replaced with Archived Content On Page

```yaml
---
import:
 - Includes/PluginReplacedArchived
removed_in_version: 2.1.0
replacement_plugins: '[content_size](/Plugins/content_size)'
---
# NZB Size
[Includes/PluginReplacedArchived](/Includes/PluginReplacedArchived){.include}
```

See result at [nzb_size](/Plugins/nzb_size).


#### Plugin Replaced, Simple Redirect
```yaml
---
import:
 - Includes/PluginReplaced
removed_in_version: 2.1.0
replacement_plugins: '[transmission](/Plugins/transmission)'
---
# Transmission RPC
[Includes/PluginReplaced](/Includes/PluginReplaced){.include}
```

See result at [transmissionrpc](/Plugins/transmissionrpc).

#### Plugin Removed with Archived Content On Page
```yaml
---
import:
 - Includes/PluginRemovedArchived
removed_in_version: 2.3.0
---
# Rlslog
[Includes/PluginRemovedArchived](/Includes/PluginRemovedArchived){.include}
```

See result at [rlslog](/Plugins/rlslog).

#### Plugin Removed
```yaml
---
import:
 - Includes/PluginRemoved
removed_in_version: 2.1.0
replacement_plugins: '[transmission](/Plugins/transmission)'
---
# Transmission RPC
[Includes/PluginRemoved](/Includes/PluginRemoved){.include}
```

No examples of this yet.
