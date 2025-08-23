---
title: Git
description: 
published: true
date: 2025-08-23T23:36:30.883Z
tags: 
editor: markdown
dateCreated: 2023-01-15T13:55:09.588Z
---

# Upgrading git checkout

>Detailed changes can be found from [ChangeLog](/ChangeLog).
{.is-info}

## Check current version

Check the latest release you have by getting new tags with `git fetch --tags` then running `git describe`.

Write this version number down somewhere.

[Backup](/Upgrade/Partial/Backup){.include}

## Upgrade GIT checkout

Git users can just run `git pull`. If the dependencies have changed, you'll also have to run `uv sync` again to upgrade them. Remember to use `--group NAME` or `--all-groups` (for everything) or `uv` will uninstall unwanted dependencies which you may actually want to keep.

[Verify](/Upgrade/Partial/Verify){.include}