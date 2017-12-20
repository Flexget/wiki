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
| **ignore_episodes_with_files** | Unmonitors any episodes with a file.  Default is False |
| **ignore_episodes_without_files** | Unmonitors any episodes without a file. Default is False | 
| **search_missing_episodes**  | Searches for missing files after applying `ignore_episodes_with_files` and `ignore_episodes_with_files`. It can be used to control which episodes Sonarr monitors after adding the series, ignoring episodes with and without files will only monitor future episodes. Default is True |
| **profile_id**  | Allows you to change the quality profile that is selected during series creation. You can find quality profile/profile ID at `http://localhost:8989/api/profile?apikey=APIKEY`. Default value is 1 |
| **season_folder**  | Allows you to set the season folder to either true or false. Default is False |
| **monitored**  | Allows you to set the whole series to either monitored or paused. If set to false you don't have to use `ignore_episodes_with_files` or `ignore_episodes_without_files`. Default is True |
| **root_folder_path**  | Allows you to set the location of the root folder path. example: `D:\Media\TV Shows` Default points to the root folder path you first setup in sonarr. |
| **series_type**  | Allows you to change the series type between `standard, daily, or anime`. Default is standard |
| **tags**  | Allows you to set tags. Has to be a number value between brackets like example: `[1,2,3,4,5]`. Tag ID's can be found at `http://localhost:8989/api/tag?apikey=APIKEY`. Requires you to have pre-setup any tags you plan on using. Default is [0] (not passing any tags) |
  
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
