---
title: service
description: 
published: true
date: 2022-09-18T05:27:11.691Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:27:09.100Z
---

# Windows Service Installer
**`WARNING:`** This plugin is not very well tested. Somebody please improve this documentation.

This CLI command can be used to install a windows service which runs the FlexGet daemon.

## Usage
### REQUIREMENTS
**`PYWIN32`**
This plugin requires pywin32 to be installed. Download [here](https://sourceforge.net/projects/pywin32/files/pywin32/Build%20220/).

**OR**

**`ACTIVEPYTHON`** Second option is to install [ActivePython](http://www.activestate.com/activepython/)

Use `flexget service --help` to get the options. Make sure you specify an username and password when installing the service.

**`Commands`**

Localhost usernames are .\

```
flexget service install --username .\johndoe --password janedoe --state auto
```



None of the options provided by `flexget service --help` seem to work currently. A workaround is to use `flexget service install` to install the basic service and then using Windows Services manager to edit the user the service is run under.

