# Medusa
This plugin creates an [Entry](/Entry) for each show in your [medusa](https://github.com/pymedusa/Medusa) show list (including ended ones).
This plugin can be used with the [discover](/Plugins/discover) or [configure_series](/Plugins/configure_series) plugins to add those shows to the shows list.

## Plugin Settings
Currently the following settings are required:


|  Option  |  Description  |
| --- | --- |
| **base_url** | This is the URL of your sickbeard installation (usually http://localhost)  |
| **username** | This is the username that you user for login   |
| **password** | This is the password of your user  |
The following settings are optional:


|  Option  |  Description  |
| --- | --- |
| **port** | This is the port used by your medusa installation (8081 by deafult)
| **include_ended** |  Decides whether to retrieve ended shows. Default is `yes`.  |
| **only_monitored** |  Retrieves only shows that are not marked as 'Paused' in sickbeard. Default is `no`.  |



### Example 1: Add all listed shows to series list
```yaml
  configure_series:
    from:
      medusa:
        base_url: http://127.0.0.1
        port: 8081
        username: USERNAME
        password: PASSWORD
```

### Example 2: Add only monitored series
```yaml
templates:
  medusa:
    configure_series:
      from:
        medusa:
          base_url: http://192.168.1.45
          port: 8081
          username: USERNAME
          password: PASSWORD
          only_monitored: yes
```
Note that by using the [configure_series](/Plugins/configure_series) plugin on a schedule you basically sync the shows on your Medusa show list with Flexget shows list. Meaning that unless you have manually set up additional shows using the [series](/Plugins/series) plugin, removing a show from Medusa will remove it from Flexget's show list as well (which can be good or bad, depending on your usage).