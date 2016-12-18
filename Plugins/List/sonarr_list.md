# Sonarr List
<div class="alert alert-success" role="info">
  
  <span class="glyphicon glyphicon glyphicon-cog"></span>
  &nbsp; This is part of [managed list](/Plugins/List) plugin system.
</div>

Creates an [Entry](/Entry) for each show in your [Sonarr](https://sonarr.tv/) show list (including ended ones by default).

This plugin can be used with the [discover](/Plugins/discover) or [configure_series](/Plugins/configure_series) plugins to add those shows to the shows list.

## Plugin Settings
Currently the following settings are required:


|  Option  |  Description  |
| --- | --- |
| **base_url** | This is the URL of your Sonarr installation (usually http://localhost). Default port is 80.  |
| **api_key** | This is API key of your Sonarr installation (can be found under setting->general->security)   |

The following settings are optional:


|  Option  |  Description  |
| --- | --- |
| **port** | This is the port used by your Sonarr installation (usually 8989). Use if port is different than 80.  |
| **include_ended** |  Decides whether to retrieve ended shows. Default is True  |
| **only_monitored** |  Retrieves only [monitored](https://github.com/Sonarr/Sonarr/wiki/Monitoring-Series-and-Episodes) shows on Sonarr. Default is False  |
| **include_data** |  Decides whether to send quality profile, cutoff quality and original show path to Flexget. Default is False. Relevant only when combining with [configure_series](https://flexget.com/wiki/Plugins/configure_series) plugin |

## Examples

### Configure series from sonarr

```yaml
get-all-shows-from-sonarr-task:
  configure_series:
    from:
      sonarr_list:
        base_url: http://localhost
        port: 8989
        api_key: MYAPIKEY1123
        include_data: yes
```

### Add series from trakt to sonarr
```yaml
trakt_list:
  account: account_name
  list: watchlist
  type: shows
accept_all: yes
list_add:
  - sonarr_list:
      base_url: http://localhost
      port: 8989
      api_key: MYAPIKEY1123
```
