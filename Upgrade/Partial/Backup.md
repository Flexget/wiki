---
title: Backup database
description: 
published: true
date: 2023-01-16T20:05:41.772Z
tags: 
editor: markdown
dateCreated: 2023-01-16T20:05:41.772Z
---

## Backup database(s) (optional)

In case you wish to roll back to previous version you will need to make backup of your database since running new version will upgrade it and downgrade is not supported.

Each configuration file has corresponding database file, so for example config.yml will have db-config.sqlite

Copy this file to backup file containing the version number you are were last using, e.g. db-config.sqlite_1.1.59