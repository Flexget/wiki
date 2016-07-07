# Configure series
Generates [series](/Plugins/series) plugin configuration from titles produced by any input. Using this doesn't prevent configuring [series](/Plugins/series) plugin additionally. 

Most commonly used with [trakt_list](/Plugins/List/trakt_list), [filesystem](/Plugins/filesystem), or [thetvdb_favorites](/Plugins/thetvdb_favorites).

## Syntax
```
configure_series:
  [settings](/settings):
    # any series option
    # e.g. quality, timeframe etc
  from:
    # any input(s)
```

### Settings
You can use any of the [settings for the series plugin](/Plugins/series#Settings) within the 'settings' block in configure_series. This section is optional, but if included, the settings will be applied to every show configured.

### From
In this section you must include one or more configured [input plugins](/Plugins#Input). The titles of the entries created by this plugin will be used as the names of the series that you desire.


## Example
Let's say you have a directory where all your series are stored in each in the own folder. Something like:

```
/media/series/pioneer one/
/media/series/south park/
```

To automatically configure series plugin with all these you could do following:

```
configure_series:
  settings:
    quality: 720p
  from:
    filesystem:
      - /media/series/
```

This will make adding new series easy too, just create new directory there :)

**NOTE:** If you need to set different options for individual series, you can do so using the [series](/Plugins/series) plugin alongside configure_series as shown in this [recipe.](/Cookbook/ForceStrictMatching)