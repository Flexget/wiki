# Third-Party Plugin Template and Instructions

This page provides and explains the template for a third-party plugin wiki page. A complete template with no explanation text is available [here](/_edit/Site/ThirdPartyPluginTemplateFull). (Copy and paste the Markdown source from that page into your plugin's wiki page. **Do not** save changes directly at that link.)

## Plugin Info
At the top, enter the link to your plugin, the plugin name (which should match the wiki page URL), and a link to where users can submit issues. If your plugin is installed as a Python package, change the text `Includes/ThirdPartyPluginInstallDotFlexget` to `Includes/ThirdPartyPluginInstallPackage` in both places where it appears in the final template. Do not otherwise modify the imports.

```yaml
---
plugin_link: "[GitHub](https://github.com/example/example-repo/blob/master/example-plugin.py)"
plugin_name: app_deluge_find
plugin_issues: "[GitHub](https://github.com/example/example-repo/issues)"
import:
- Includes/ThirdPartyPluginWarning
- Includes/ThirdPartyPluginInstallDotFlexget
- Includes/ThirdPartyPluginIssues
---
```

## Title and Description
The `Plugin Title` should generally be the same as the name, with underscores removed and words capitalized. Enter a general description of the plugin. Do not modify the line below the plugin title.

```markdown
# Plugin Title
{{> Includes/ThirdPartyPluginWarning }}


This is where your plugin description goes.
```


## Installation
Install instructions are provided in an imported bit of text. If your plugin is installed as a Python package, change the text `Includes/ThirdPartyPluginInstallDotFlexget` to `Includes/ThirdPartyPluginInstallPackage` in both places where it appears in the final template. Do not otherwise modify this line.
```yaml
{{> Includes/ThirdPartyPluginInstallDotFlexget }}
```

## Usage
Describe the plugin's usage scenarios. Include example configurations.

If your plugin takes options, include a table that describes them. Required options should be in **bold**.

For formatting reasons, an extra `\` (backslash) is inserted before the three backticks on two lines in the example below. Remove this backslash on your actual plugin page.

```markdown
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
\```

Example with optional features:
```yaml
my_plugin:
  required_option: blue
  optional_option: green
\```
```

## Issues
The issues link is provided in an imported bit of text. The link to your issues page is designated in the first section. Do not modify this section.

```
{{> Includes/ThirdPartyPluginIssues }}
```