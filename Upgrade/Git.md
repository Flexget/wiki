---
title: Git
description: 
published: true
date: 2023-01-15T14:07:03.111Z
tags: 
editor: markdown
dateCreated: 2023-01-15T13:55:09.588Z
---

# Upgrading git checkout

>Detailed changes can be found from [ChangeLog](/ChangeLog).
{.is-info}

## Check current version

Check the latest release you have by getting new tags with `git fetch --tags` then running `git describe`

## Upgrade GIT checkout

Git users can just run `git pull`. If the dependencies have changed, you'll also have to run `bin/pip install -e .` again to upgrade them.

## Verify

Check if your configuration file is still valid, there may have been some changes to it.

```cmd
flexget check
```

If your configuration doesn't pass check, have a look at [upgrade actions](/UpgradeActions) to see if there are any actions you must take. The behavior of certain plugins may also have changed, so check [upgrade actions](/UpgradeActions) even if your config is passing.

For example, if you were running 3.1.2 follow all the steps above this revision.
