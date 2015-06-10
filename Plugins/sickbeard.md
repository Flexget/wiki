= Sickbeard=
This plugin creates an [wiki:Entry Entry] for each show in your [http://sickbeard.com/ sickbeard] show list (including ended ones).
This plugin can be used with the [wiki:Plugins/discover discover] or [wiki:Plugins/configure_series configure_series] plugins to add those shows to the shows list.

== Plugin Settings ==

Currently the following settings are required:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''base_url'''||This is the URL of your sickbeard installation (usually http://localhost) ||
||'''api_key'''||This is API key of your sickbeard installation (can be found under config->general->API)  ||
}}}
The following settings are optional:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''port'''||This is the port used by your sickbeard installation (8081 by deafult). Use if your Sickbeard port is different than 80 ||
||'''include_ended'''|| Decides whether to retrieve ended shows. Default is True ||
||'''only_monitored'''|| Retrieves only shows that are not marked as 'Paused' in sickbeard. Default is False ||
}}}
=== Example: Add all listed shows to series list ===
{{{
  get-all-shows-from-sickbeard-task:
      configure_series:
            settings:
              quality:
                - 720p
            from:
              sickbeard:
                base_url: http://localhost
                port: 8531
                api_key: MYAPIKEY1123
}}}

Note that by using the [wiki:Plugins/configure_series configure_series] plugin on a schedule you basically sync the shows on your Sickbeard show list with Flexget shows list. Meaning that unless you have manually set up additional shows using the [wiki:Plugins/series series] plugin, removing a show from Sickbeard will remove it from Flexget's show list as well (which can be good or bad, depending on your usage).