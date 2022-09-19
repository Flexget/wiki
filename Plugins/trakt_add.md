---
title: trakt_add
description: 
published: true
date: 2022-09-18T05:14:56.673Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:14:54.058Z
---

# Trakt Add 
[Includes/PluginReplacedArchived](/Includes/PluginReplacedArchived){.include}

**IMPORTANT:**

* Please see [trakt](/Plugins/trakt) on how to authorize Flexget to access your private Trakt.tv account.**

This plugin will add accepted movies/tv episodes to one of your [trakt.tv](http://trakt.tv) lists.

This plugin can be added to any of your tasks that deal with movies/series, or it can be used with the [filesystem](/Plugins/filesystem) plugin to add all your already acquired episodes/movies on trakt.tv to a specified list.

Please note that `account` is **required**.

**Configuration:**

```text
trakt_add:
  username: <trakt username>
  account: <flexget account name>
  list: <list name>
  type: [auto|shows|seasons|episodes|movies]
```

The `list` option can be one of the built in trakt lists, `collection`, `watched`, or `watchlist`, or the name of one of your custom trakt lists.

Setting the `type` option to anything but auto (the default) forces entries to be of a given item type or not be added.
