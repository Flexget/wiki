---
title: app_deluge_find
description: 
published: true
date: 2022-09-18T05:05:32.739Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:02:06.727Z
---

# Find Deluge.app

> This plugin should no longer be needed as of FlexGet 2.16.0
{.is-warning}

[Includes/ThirdPartyPluginWarning](/Includes/ThirdPartyPluginWarning){.include}


This plugin makes FlexGet work with [Deluge.app](http://dev.deluge-torrent.org/wiki/Download#AppleMacOSX) on macOS (instead of needing to have the `deluge` package and all of its dependencies installed in `site-packages`).

It does this by modifying the system `$PATH` when the plugin is initialized to reference the deluge package that is contained within `/Applications/Deluge.app`. The contrived name of the plugin is to ensure it runs _before_ the normal Deluge plugin, so that when that plugin tries to find the `deluge` package, it suceeds.

[Includes/ThirdPartyPluginInstallDotFlexget](/Includes/ThirdPartyPluginInstallDotFlexget){.include}

## Usage
Add the plugin to any task which uses the [`deluge`](/Plugins/deluge) or [`from_deluge`](/Plugins/from_deluge) plugins. There are no options.
```yaml
app_deluge_find: yes
```

[Includes/ThirdPartyPluginIssues](/Includes/ThirdPartyPluginIssues){.include}