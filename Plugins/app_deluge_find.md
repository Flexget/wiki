---
plugin_link: "[GitHub](https://github.com/tubedogg/flexget-plugins/blob/master/app_deluge_find.py)"
plugin_name: app_deluge_find
plugin_issues: "[GitHub](https://github.com/tubedogg/flexget-plugins/issues)"
import:
- Includes/ThirdPartyPluginWarning
- Includes/ThirdPartyPluginInstallDotFlexget
- Includes/ThirdPartyPluginIssues
---
# Find Deluge.app
{{> Includes/ThirdPartyPluginWarning }}


This plugin makes FlexGet work with [Deluge.app](http://dev.deluge-torrent.org/wiki/Download#AppleMacOSX) on macOS (instead of needing to have the `deluge` package and all of its dependencies installed in `site-packages`).

It does this by modifying the system `$PATH` when the plugin is initialized to reference the deluge package that is contained within `/Applications/Deluge.app`. The contrived name of the plugin is to ensure it runs _before_ the normal Deluge plugin, so that when that plugin tries to find the `deluge` package, it suceeds.

{{> Includes/ThirdPartyPluginInstallDotFlexget }}

## Usage
Add the plugin to any task which uses the [`deluge`](/Plugins/deluge) or [`from_deluge`](/Plugins/from_deluge) plugins. There are no options.
```yaml
app_deluge_find: yes
```

{{> Includes/ThirdPartyPluginIssues }}