# Sickbeard
This plugin creates an [Entry](/Entry) for each show in your [sickbeard](http://sickbeard.com/) show list (including ended ones).
This plugin can be used with the [discover](/Plugins/discover) or [configure_series](/Plugins/configure_series) plugins to add those shows to the shows list.

## Plugin Settings
Currently the following settings are required:


|  Option  |  Description  |
| --- | --- |
| **base_url** | This is the URL of your sickbeard installation (usually http://localhost)  |
| **api_key** | This is API key of your sickbeard installation (can be found under config->general->API)   |

The following settings are optional:


|  Option  |  Description  |
| --- | --- |
| **port** | This is the port used by your sickbeard installation (8081 by deafult). Use if your Sickbeard port is different than 80  |
| **include_ended** |  Decides whether to retrieve ended shows. Default is True  |
| **only_monitored** |  Retrieves only shows that are not marked as 'Paused' in sickbeard. Default is False  |
| **include_data** |  Will return the show quality profile. Default is false  |


### Example 1: Add all listed shows to series list
```yaml
configure_series:
  settings:
    quality:
      - 720p
  from:
    sickbeard:
      base_url: http://localhost
      port: 8531
      api_key: MYAPIKEY1123
```

### Example 2: Add monitored, non-ended shows with their quality

```yaml
configure_series:
  from:
    sickbeard:
      base_url: http://localhost
      port: 8531
      api_key: MYAPIKEY1123
      include_ended: no
      only_monitored: yes
      include_data: yes
```

Note that by using the [configure_series](/Plugins/configure_series) plugin on a schedule you basically sync the shows on your Sickbeard show list with FlexGet shows list. Meaning that unless you have manually set up additional shows using the [series](/Plugins/series) plugin, removing a show from Sickbeard will remove it from FlexGet's show list as well (which can be good or bad, depending on your usage).