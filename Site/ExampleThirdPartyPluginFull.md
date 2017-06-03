---
plugin_link: "[GitHub](https://github.com/example/example-repo/blob/master/example-plugin.py)"
plugin_name: my_plugin
plugin_issues: "[GitHub](https://github.com/example/example-repo/issues)"
import:
- Includes/ThirdPartyPluginWarning
- Includes/ThirdPartyPluginInstallDotFlexget
- Includes/ThirdPartyPluginIssues
---
# Plugin Title
{{> Includes/ThirdPartyPluginWarning }}


Plugin description text.

{{> Includes/ThirdPartyPluginInstallDotFlexget }}

## Usage
Usage description text.

| **Option** | **Description** |
| --- | --- |
| **required_option** | This option makes the plugin do XYZ. |
| optional_option | If present, this option will cause ABC to happen. |

Example config:
```yaml
my_plugin:
  required_option: blue
```

Example with optional features:
```yaml
my_plugin:
  required_option: blue
  optional_option: green
```

{{> Includes/ThirdPartyPluginIssues }}