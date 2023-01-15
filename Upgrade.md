---
title: Upgrade
description: 
published: true
date: 2023-01-15T14:04:30.142Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:52:13.370Z
---

# Upgrading

## Backup database(s) (optional)

In case you wish to roll back to previous version you will need to make backup of your database since running new version will upgrade it and downgrade is not supported.

Each configuration file has corresponding database file, so for example config.yml will have db-config.sqlite

Copy this file to backup file containing the version number you are were last using, e.g. db-config.sqlite_1.1.59


## Choose installation method

[PIP installation](Uprade/Pip)
[GIT installation](Uprade/Git)


### Problems ?

If you encounter problems, there are ways to get [help](/NeedHelp) !

If you receive errors about database upgrades please report them via a [ticket](https://github.com/Flexget/Flexget/issues). If you do not care about the history for that plugin, you can reset the database for that plugin with `--reset-plugin PLUGINNAME` to get it working again.
