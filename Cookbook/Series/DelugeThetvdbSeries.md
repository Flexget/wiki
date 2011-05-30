= Advanced Deluge and thetvdb features =

{{{
presets:
  tv:
    thetvdb_favorites:
      account_id: 230B039A30
      quality: 720p
    exists_series:
      - /media/tv
      - /media/incomplete
    thetvdb_lookup: yes
    set:
      path: /media/incomplete
      movedone: "/media/tv/{{ series_name }}/Season {{ series_season }}"
      content_filename: >
        {{ series_name }} - {{ series_id }}
        {% if ep_name|default(False) %}- {{ ep_name }} {% endif %}- {{ quality|upper }}
        {% if proper %}- proper{% endif %}
    deluge:
      main_file_only: yes

feeds:
  betterfeed:
    priority: 1
    preset: tv
    rss: http://feed1.com/feed.xml

  backupfeed:
    priority: 2
    preset: tv
    rss: http://feed2.com/feed.xml
}}}

First we create a preset called 'tv' that holds all the plugin information we need to grab our series. Inside the tv preset here is what is happening:
 - The [wiki:Plugins/thetvdb_favorites thetvdb_favorites] plugin automatically configures the [wiki:Plugins/series series] plugin to download all the shows you have marked as a favorite on thetvdb.com. You can specify all of the options of the series plugin here, this example shows the quality option. Your account_id can be found on your account page at thetvdb.com
 - The [wiki:Plugins/exists_series exists_series] plugin will make sure we don't already have this episode in our tv library or currently downloading folder
 - We enable the [wiki:Plugins/thetvdb_lookup thetvdb_lookup] plugin to pull the name of the episode from thetvdb.com, we use this info below in {{{content_filename}}}
 - We use the [wiki:Plugins/set set] plugin to define templates for:
  - {{{movedone}}}: Deluge will move the completed files to this location. We use variable substitution to put the files in their own series and season folders
  - [wiki:Plugins/deluge#ContentRenaming content_filename]: This will cause the largest file inside the torrent (the actual show) to be renamed to our naming standard. An alternative [http://www.yaml.org/spec/current.html#id2503232 yaml syntax] for multi-line strings without quotes is used here. With this syntax each newline in the string becomes a space. We use more of the jinja2 features to format the name depending on whether an ep_name was actually retrieved, and whether this episode was a proper. 
 - We enable the [wiki:Plugins/deluge deluge] plugin, to recieve our torrents. Options:
  - {{{path}}}: Deluge will download the torrent to this location
  - {{{main_file_only}}}: All other files but main (largest) will be set to 'do not download' in Deluge. (If you use the [http://dev.deluge-torrent.org/wiki/Plugins#DelugePlugins3rdParty delete partials Deluge plugin] these files can be cleaned up when you remove the torrent from Deluge.) 

The result of setting the movedone and content_filename using string replacement means that all your shows will end up like this example:
 /media/tv/Lost/Season 1/Lost - S01E03 - Tabula Rasa - 720P.mkv
You can adjust those lines to match your naming standard.

In the feeds section, we define 2 feeds in case one is faster, or one goes down. The [wiki:Plugins/priority priority] plugin is used to make sure that your preferred feed is checked before your backup feed when !FlexGet is run.

= Advanced Deluge and thetvdb features run on ver. 1.0r2245 =

{{{
presets:
  tv:
    import_series:
      from:
        thetvdb_favorites:
          account_id: 230B039A30
          #strip_dates: yes #optional
          #quality: 720p #quality does not work here#
    exists_series:
      - /media/tv
      - /media/incomplete
    thetvdb_lookup: yes
    set:
      quality:
        min: sdtv
        max: 720p
      #quality: 720p  #you could accept one quality only if you want#
      path: /media/incomplete
      movedone: "/media/tv/{{ series_name }}/Season {{ series_season }}"
      content_filename: >
        {{ series_name }} - {{ series_id }}
        {% if ep_name|default(False) %}- {{ ep_name }} {% endif %}- {{ quality|upper }}
        {% if proper %}- proper{% endif %}
    deluge:
      main_file_only: yes
      user: xxxx
      pass: yyyy

feeds:
  betterfeed:
    priority: 1
    preset: tv
    rss: http://feed1.com/feed.xml

  backupfeed:
    priority: 2
    preset: tv
    rss: http://feed2.com/feed.xml
}}}

= Thetvdb Favorites =

This plugin will create a list of entries for all the shows you have marked as favorites at [http://thetvdb.com]. If thetvdb goes down, the last known list of favorites will be used until it comes back online. This plugin can be used from the [wiki:Plugins/import_series import_series] plugin to automatically configure !FlexGet to download all of your tvdb favorites.

You configure thetvdb_favorites plugin with your account id at thetvdb. You can find it on the [http://thetvdb.com/?tab=userinfo account tab] after you log in.

''' Example '''

{{{
import_series:
  from:
    thetvdb_favorites:
      account_id: 320D93B3A1
}}}

== Strip Dates Option ==
If the {{{strip_dates}}} option is specified, the trailing year will be stripped from series names that include them. For example, "Merlin (2008)" would become just "Merlin".

''' Example '''
{{{
thetvdb_favorites:
  account_id: 320D93B3A1
  strip_dates: yes
}}}

== Series Settings ==
You can use any of the [wiki:Plugins/series#Settings settings] of the series plugin with the [wiki:Plugins/import_series import_series] plugin, as shown below.

''' Example '''

{{{
import_series:
  from:
    thetvdb_favorites:
      account_id: 320D93B3A1
  settings:
    timeframe: 12 hours
    quality: 720p
    propers: 3 days
}}}