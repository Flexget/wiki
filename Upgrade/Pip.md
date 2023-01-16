---
title: Pip
description: 
published: true
date: 2023-01-16T19:54:20.786Z
tags: 
editor: markdown
dateCreated: 2023-01-15T13:59:04.528Z
---

# Upgrading PIP installation

>Detailed changes can be found from [ChangeLog](/ChangeLog).
{.is-info}

## Check current version

Start by checking what version you currently have with command:

```bash
flexget -V
```

Write your current version down somewhere.

## Upgrade

If you are using cron and have short cron interval, comment FlexGet out from the cron. If you are running the daemon, you should [stop the daemon](/Daemon) until the upgrade is complete and you verify your config file works with the updated version.

There has been alot of errors arising from setuptools package being out of date and failing an upgrade.
Please make sure to upgrade setuptools.

> Note: On some environments, pip might be available under name pip3 to differentiate it from Python 2. Check [Problems with pip](/PipProblems) page if issues arise.
{.is-info}

```cmd
pip install --upgrade setuptools
```

Upgrade FlexGet

```cmd
pip install --upgrade flexget
```

## Verify

Check if your configuration file is still valid, there may have been some changes to it.

```cmd
flexget check
```

If your configuration doesn't pass check, have a look at [upgrade actions](/UpgradeActions) to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [upgrade actions](/UpgradeActions) even if your config is passing.

For example, if you were running 3.1.2 follow all the steps above this revision.