= Advanced Deluge and thetvdb features =

{{{
presets:
  tv:
    thetvdb_favorites:
      account_id: 230B039A30
    series:
      settings:
        thetvdb:
          quality: 720p
    exists_series:
      - /media/tv
      - /media/incomplete
    thetvdb_lookup: yes
    set:
      path: /media/incomplete
      movedone: /media/tv/%(series_name)s/Season %(series_season)d
      content_filename: "%(series_name)s - S%(series_season)02dE%(series_episode)02d - %(ep_name)s - %(quality)s"
    deluge: yes
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
 - The thetvdb_favorites plugin automatically configures the series plugin to download all the shows you have marked as a favorite on thetvdb.com Your account_id can be found on your account page at thetvdb.com
 - We configure the series plugin with a series group called 'thetvdb'. This is the name of the series group that thetvdb_favorites will merge your series into. We do this, so that we can define the quality that we want for the series.
 - The exists_series plugin will make sure we don't already have this episode in our tv library or currently downloading folder
 - We enable the thetvdb_lookup plugin to pull the name of the episode from thetvdb.com, we use this info below in content_filename
 - We use the set plugin to configure the:
  - path: deluge will download the torrent to this location
  - movedone: deluge will move the completed files to this location, we use string replacement to put the files in their own series and season folders
  - content_filename: This will cause the largest file inside the torrent (the actual show) to be renamed to our naming standard.
 - We enable the deluge plugin, to recieve our torrents

The result of setting the movedone and content_filename using string replacement means that all your shows will end up like this example:
  /media/tv/Lost/Season 1/Lost - S01E03 - Tabula Rasa - 720p.avi

In the feeds section, we define 2 feeds in case one is faster, or one goes down. The priority plugin is used to make sure that your preferred feed is checked before your backup feed when flexget is run.