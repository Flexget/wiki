= TheTVDB Lookup =

This plugin looks up more information from thetvdb.com about any entries that !FlexGet has identified as series. (with a season and episode number) thetvdb_lookup will populate several more entry fields that can be used in other plugins.

||series_name_tvdb||Series name provided by thetvdb||
||series_rating||Series rating||
||series_status||Series status(Continuing or Ended)||
||series_runtime||Series runtime in minutes)||
||series_first_air_date||Series premier date||
||series_air_time||Series air time||
||series_content_rating||Series content ration||
||series_genres||Series genres||
||series_network||Series network||
||series_banner_url||Series banenr url||
||series_fanart_url||Series fanart url||
||series_poster_url||Series poster url||
||series_airs_day_of_week||Series airs date of the week||
||series_actors||Series actors||
||series_language||Series language(en, fr, etc.)||
||imdb_url||Series imdb url||
||zap2it_id||||
||ep_name||Episode name||
||ep_overview||Episode plot||
||ep_director||Episode director||
||ep_writer||Episode writer||
||ep_air_date||Episode air date||
||ep_rating||Episode rating||
||ep_guest_stars||Episode guest stars||
||ep_image_url||Episode image url||

'''Example:'''

The most common use is to look up an episode title that can be used to format a pretty filename. This example uses {{{ep_name}}} as parsed by thetvdb_lookup in the [wiki:Plugins/set set] plugin to set {{{content_filename}}} (which the [wiki:Plugins/deluge deluge] plugin uses to rename the main file within a torrent.) The 'default' jinja filter is used to insert 'Unknown' if thetvdb_lookup fails to get an ep_name for the entry.
{{{
thetvdb_lookup: yes
set:
  content_filename: "{{ series_name }} - {{ series_id }} - {{ ep_name|default('Unknown') }}  - {{ quality|upper }}"
}}}