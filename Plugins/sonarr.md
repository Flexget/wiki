= Sonarr=
This plugin creates an [wiki:Entry Entry] for each show in your [https://sonarr.tv/ Sonarr] show list (including ended ones by default).
This plugin can be used with the [wiki:Plugins/discover discover] or [wiki:Plugins/configure_series configure_series] plugins to add those shows to the shows list.

== Plugin Settings ==

Currently the following settings are required:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''base_url'''||This is the URL of your Sonarr installation (usually http://localhost). Default port is 80. ||
||'''api_key'''||This is API key of your Sonarr installation (can be found under setting->general->security)  ||
}}}
The following settings are optional:
{{{#!div style="margin-left: 25px"
||= Option =||= Description =||
||'''port'''||This is the port used by your Sonarr installation (usually 8989). Use if port is different than 80. ||
||'''include_ended'''|| Decides whether to retrieve ended shows. Default is True ||
||'''only_monitored'''|| Retrieves only [https://github.com/Sonarr/Sonarr/wiki/Monitoring-Series-and-Episodes monitored] shows on Sonarr. Default is False ||
||'''include_data'''|| Decides whether to send quality profile, cutoff quality and original show path to Flexget. Default is False. Show path will appear under `sonarr_show_path`.||

'''Note:''' You can use `sonarr_show_path` with plugins like `deluge` or `utorrent` to automatically set the download path to the original show locations.
=== Example: Add all listed shows to series list ===
{{{
  get-all-shows-from-sonarr-task:
      configure_series:
            from:
              sonarr:
                base_url: http://localhost
                port: 8989
                api_key: MYAPIKEY1123
                include_data: yes
}}}

Note that by using the [wiki:Plugins/configure_series configure_series] plugin on a schedule you basically sync the shows on your Sonarr show list with Flexget shows list. Meaning that unless you have manually set up additional shows using the [wiki:Plugins/series series] plugin, removing a show from Sonarr will remove it from Flexget's show list as well (which can be good or bad, depending on your usage).