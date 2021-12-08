# Wiki `import`

## Using Import
Import of other wiki pages can be done on any page by adding this block at the top, above all other content:
```yaml
---
import:
 - Path/To/OtherPage
---
```

Then, in the body of the page, add this where you want the content to show up. Note it must exactly match the path as entered in the `import` statement above.

```markdown
{{> /Path/To/OtherPage }}
```

If you are adding something that will be used on multiple pages, please add it in the [Includes](/Includes/) directory. Click the Index button on that page (at the top-left next to "FLEXGET") to view existing files.

## Plugin information

### Requires additional libraries via pip
```yaml
---
import:
 - Includes/PluginRequiresPip
packages: a b c
---

{{> Includes/PluginRequiresPip }}
```

## Info

```yaml
---
import:
 - Includes/PluginInfo
info: text here
---

{{> Includes/PluginInfo }}

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
{{> Includes/PluginReplacedArchived }}
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
{{> Includes/PluginReplaced }}
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
{{> Includes/PluginRemovedArchived }}
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
{{> Includes/PluginRemoved }}
```

No examples of this yet.
