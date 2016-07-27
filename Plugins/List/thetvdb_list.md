# TheTVDB List

This plugin is a [list](/Plugins/List) plugin.

This plugin is mainly used from the [configure_series](/Plugins/configure_series) plugin to automatically configure FlexGet to download all of your TVDB favorites. The plugin can work as input that returns entries for all the shows you have marked as favorites at [http://thetvdb.com](/http://thetvdb.com). If TheTVDB goes down, the last known list of favorites will be used until it comes back online. 

You can also add and remove shows from it, like any other list plugin.

You configure thetvdb_list plugin with your username and account id at TheTVDB . You can find it on the [account tab](http://thetvdb.com/?tab=userinfo) after you log in.

** Example **

```yaml
configure_series:
  from:
    thetvdb_list:
      username: <username>
      account_id: <account identifier>
```

## Strip Dates Option
If the `strip_dates` option is specified, the trailing year will be stripped from series names that include them. For example, "Merlin (2008)" would become just "Merlin".

** Example **
```yaml
thetvdb_list:
  username: <username>
  account_id: <account identifier>
  strip_dates: yes
```

## Series Settings
You can use any of the [settings](/Plugins/series#Settings) of the series plugin with the [configure_series](/Plugins/configure_series) plugin, as shown below.

** Example **

```yaml
configure_series:
  from:
    thetvdb_list:
      username: <username>
      account_id: <account identifier>
  settings:
    timeframe: 12 hours
    target: 720p
    propers: 3 days
```

## Adding and removing
You can add, remove or match according to your favorites list. Note that entries must contain `tvdb_id` to operate on the list, so adding a lookup plugin like [thetvdb_lookup](/Plugins/thetvdb_lookup) to the task may be required.

** Example: Adding to TheTVDB list from Trakt List **
```yaml
trakt_list: <opts>
accept_all: yes
thetvdb_lookup: yes
list_add:
  - thetvdb_list:
      username: username
      account_id: account_identifier
seen: local
```


