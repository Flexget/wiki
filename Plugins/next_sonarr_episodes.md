= Next Sonarr Episodes =

This plugin creates an [wiki:Entry Entry] for the first missing episode for every show as defined in [http://sonarr.tv Sonarr] .

This plugin can be used in combination with several plugins, like [wiki:Plugins/discover discover] to search for new episodes to download, or [wiki:Plugins/set_series_begin set_series_begin] to reset the first episode for configured series, and so on.[[BR]].

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
||'''page_size'''|| Defines the number of results to be retunred with every page of the API request. Set to 50 by default. Can be changed in order to resolve performance issues.

=== Example: set_series_begin plugin ===

This example shows how the next_sonarr_episodes plugin could be used with the [wiki:Plugins/set_series_begin set_series_begin] plugin in order to set the first episode for all monitored and running shows as defined in [http://sonarr.tv Sonarr]:

{{{
  set-series-begin-from-sonarr:
      next_sonarr_episodes:
        base_url: '{{ secrets.credentials.sonarr.url }}'
        port: 8989
        api_key: '{{ secrets.credentials.sonarr.api_key }}'
        include_ended: false
      accept_all: yes
      set_series_begin: yes
}}}

=== Example: discover_plugin === 

This example shows how the next_sonarr_episodes plugin could be used with the [wiki:Plugins/discover discover] plugin in order to download the first missing episode for all monitored and running shows as defined in [http://sonarr.tv Sonarr]:

{{{
 discover_from_sonarr_task:
      discover:
        what:
          - next_sonarr_episodes:
              base_url: '{{ secrets.credentials.sonarr.url }}'
              port: 8989
              api_key: '{{ secrets.credentials.sonarr.api_key }}'
              include_ended: false
        from:
          - kat:
              verified: yes
      all_series: yes
      download: /download
}}}