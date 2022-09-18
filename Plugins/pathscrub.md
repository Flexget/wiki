---
title: pathscrub
description: 
published: true
date: 2022-09-18T05:09:36.544Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:09:33.978Z
---

# Pathscrub
This plugin is used by plugins that create files. (currently: download, move, deluge, transmission) It automatically removes any invalid characters for the current OS from generated filenames.

**Note:** You do not need to include this plugin in your config, unless you would like the generated filenames to be compatible with another OS than the one FlexGet is running on. (e.g. files need valid Windows names to be accessed over a samba share, or you are adding files to a remote deluge/transmission daemon on another OS)

To make filenames compatible with another OS, it can be configured like this:
```
pathscrub: windows
```
Valid OS options are: `windows`, `mac`, `linux`

Windows has the strictest limitations on filenames, so using this mode will make filenames compatible with all OSs. Linux has no restrictions on filenames, so no changes to paths will be made in this mode.