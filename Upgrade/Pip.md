---
title: Pip
description: 
published: true
date: 2023-01-16T20:06:55.478Z
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

[Backup](/Upgrade/Partial/Backup){.include}

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

[Verify](/Upgrade/Partial/Verify){.include}