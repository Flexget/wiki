---
title: thetvdb_list
description: 
published: true
date: 2022-09-18T05:25:29.352Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:25:26.658Z
---

# TheTVDB List

> This is part of [managed list](/Plugins/List) plugin system.
{.is-success}

This plugin is mainly used from the [configure_series](/Plugins/configure_series) plugin to automatically configure FlexGet to download all of your TVDB favorites. The plugin can work as input that returns entries for all the shows you have marked as favorites at [Member Favorites](https://www.thetvdb.com/member/favorites). If TheTVDB goes down, the last known list of favorites will be used until it comes back online. 

You can also add and remove shows from it, like any other managed list plugin.

You configure thetvdb_list plugin with your username, account id and generated api key at TheTVDB . You can find this information on the [Member API](https://www.thetvdb.com/member/api) page after you log in. You will need to generate an api key on that page if you have not already done so.

|Option|Description|
|---|---|
|strip_dates|If set to `yes` the trailing year will be stripped from series names that include them. For example, `Merlin (2008)` would become just `Merlin`.|
|username|Get this from the [Dashboard -  API keys](https://thetvdb.com/dashboard/account/apikey) page|
|account_id|Get this from the [Account - Edit Information](https://thetvdb.com/dashboard/account/editinfo) page|
|api_key|Get this from the [Dashboard - API keys](https://thetvdb.com/dashboard/account/apikey) page|
|language|Specify the language code to get translations of series titles. (_default_: en)|

## Examples

### As simple input

```yaml
thetvdb_list:
  username: <username>
  account_id: <account_id>
  api_key: <api_key>
  strip_dates: yes
```

### Configure series plugin from thetvdb

You can use any of the [settings](/Plugins/series#Settings) of the series plugin with the [configure_series](/Plugins/configure_series) plugin, as shown below.

```yaml
configure_series:
  from:
    thetvdb_list:
      username: <username>
      account_id: <account_id>
      api_key: <api_key>
  settings:
    timeframe: 12 hours
    target: 720p
    propers: 3 days
```

### Add to thetvdb from trakt

You can add, remove or match according to your favorites list. Note that entries must contain `tvdb_id` to operate on the list, so adding a lookup plugin like [thetvdb_lookup](/Plugins/thetvdb_lookup) to the task may be required.

This would import all series from trakt_list and add them to yout tvdb_list.

```yaml
trakt_list: <opts>
accept_all: yes
thetvdb_lookup: yes
list_add:
  - thetvdb_list:
      username: <username>
      account_id: <account_id>
      api_key: <api_key>
seen: local
```


