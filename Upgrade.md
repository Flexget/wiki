---
title: Upgrade
description: 
published: true
date: 2022-12-06T00:06:10.355Z
tags: 
editor: markdown
dateCreated: 2022-09-18T04:52:13.370Z
---

# Upgrading

>Detailed changes can be found from [ChangeLog](/ChangeLog).
{.is-info}

## Check current version

Write your current version down somewhere.

### Installed via PIP
Start by checking what version you currently have with command:

```
flexget -V
```

### Installed via GIT

Check the latest release you have by getting new tags with `git fetch --tags` then running `git describe`

### Backup database(s) (optional)

In case you wish to roll back to previous version you will need to make backup of your database since running new version will upgrade it and downgrade is not supported.

Each configuration file has corresponding database file, so for example config.yml will have db-config.sqlite

Copy this file to backup file containing the version number you are were last using, e.g. db-config.sqlite_1.1.59

## Upgrade with PIP

If you have followed normal installation procedure follow this.
If you are using cron and have short cron interval, comment FlexGet out from the cron. If you are running the daemon, you should [stop the daemon](/Daemon) until the upgrade is complete and you verify your config file works with the updated version.

There has been alot of errors arising from setuptools package being out of date and failing an upgrade.
Please make sure to upgrade setuptools.

> Note: On some environments, pip might be available under name pip3 to differentiate it from Python 2. Check [Problems with pip](/PipProblems) page if issues arise.
{.is-info}

```cmd
pip install --upgrade flexget
```

Upgrade FlexGet

```cmd
pip install --upgrade flexget
```

## Upgrade GIT checkout

Git users can just run `git pull`. If the dependencies have changed, you'll also have to run `bin/pip install -e .` again to upgrade them.

## Verify

Check if your configuration file is still valid, there may have been some changes to it.

```cmd
flexget check
```

If your configuration doesn't pass check, have a look at [upgrade actions](/UpgradeActions) to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [upgrade actions](/UpgradeActions) even if your config is passing.

For example, if you were running 3.1.2 follow all the steps above this revision.

### Problems ?

If you encounter problems, there are ways to get [help](/NeedHelp) !

If you receive errors about database upgrades please report them via a [ticket](https://github.com/Flexget/Flexget/issues). If you do not care about the history for that plugin, you can reset the database for that plugin with `--reset-plugin PLUGINNAME` to get it working again.
