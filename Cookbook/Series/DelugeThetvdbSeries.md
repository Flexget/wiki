---
title: DelugeThetvdbSeries
description: 
published: true
date: 2022-09-18T05:20:39.173Z
tags: 
editor: markdown
dateCreated: 2022-09-18T05:20:36.560Z
---

# Advanced Deluge and thetvdb features
```
templates:
  tv:
    configure_series:
      from:
        thetvdb_favorites:
          account_id: 230B039A30
      settings:
        quality: 720p
    exists_series:
      - /media/tv
      - /media/incomplete
    thetvdb_lookup: yes
    set:
      path: /media/incomplete
      movedone: "/media/tv/{{ series_name }}/Season {{ series_season }}"
      content_filename: |
        {{ series_name }} - {{ series_id }}
        {% if tvdb_ep_name|default(False) %} - {{ tvdb_ep_name }} {% endif %} - {{ quality|upper }}
        {% if proper_count %} - proper{% if proper_count > 1 %}{{ proper_count }}{% endif %}{% endif %}
    deluge:
      main_file_only: yes

tasks:
  betterfeed:
    priority: 1
    template: tv
    rss: http://feed1.com/feed.xml

  backupfeed:
    priority: 2
    template: tv
    rss: http://feed2.com/feed.xml
```

First we create a template called 'tv' that holds all the plugin information we need to grab our series. Inside the tv template here is what is happening:
 - The [configure_series](/Plugins/configure_series) plugin automatically configures the [series](/Plugins/series) plugin to download all the shows provided by another input plugin. We are using [thetvdb_favorites](/Plugins/thetvdb_favorites) under the `from` key to input any shows you have marked as a favorite on thetvdb.com. Your account_id can be found on your account page at thetvdb.com You can specify all of the options of the series plugin under the `settings` key, this example shows the quality option.
 - The [exists_series](/Plugins/exists_series) plugin will make sure we don't already have this episode in our tv library or currently downloading folder
 - We enable the [thetvdb_lookup](/Plugins/thetvdb_lookup) plugin to pull the name of the episode from thetvdb.com, we use this info below in `content_filename`
 - We use the [set](/Plugins/set) plugin to define templates for:
  - `movedone`: Deluge will move the completed files to this location. We use variable substitution to put the files in their own series and season folders
  - [content_filename](/Plugins/deluge#ContentRenaming): This will cause the largest file inside the torrent (the actual show) to be renamed to our naming standard. An alternative [yaml syntax](http://www.yaml.org/spec/current.html#id2503232) for multi-line strings without quotes is used here. With this syntax each newline in the string becomes a space. We use more of the jinja2 features to format the name depending on whether a tvdb_ep_name was actually retrieved, and whether this episode was a proper. 
 - We enable the [deluge](/Plugins/deluge) plugin, to recieve our torrents. Options:
  - `path`: Deluge will download the torrent to this location
  - `main_file_only`: All other files but main (largest) will be set to 'do not download' in Deluge. (If you use the [delete partials Deluge plugin](http://dev.deluge-torrent.org/wiki/Plugins#DelugePlugins3rdParty) these files can be cleaned up when you remove the torrent from Deluge.) 

The result of setting the movedone and content_filename using string replacement means that all your shows will end up like this example:
 /media/tv/Lost/Season 1/Lost - S01E03 - Tabula Rasa - 720P.mkv
You can adjust those lines to match your naming standard.

In the tasks section, we define 2 tasks in case one is faster, or one goes down. The [priority](/Plugins/priority) plugin is used to make sure that your preferred feed is checked before your backup feed when FlexGet is run.