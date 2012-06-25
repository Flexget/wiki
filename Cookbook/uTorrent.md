== uTorrent example ==

This is an example how to use uTorrent with flexget and take advantage of dynamic folders at Windows 7. This is not the right and definitive way to configure uTorrent, but it's a working example.

== FlexGet configuration ==

Let's start with config:

{{{
feeds:
  movies:
    rss: http://some.tracker.feed.com
    
    # Download path defined here can be used later as %(path)s variable
    set:
      path: C:\Movies

    # Download torrents to
    download: 
      path: C:\Movies
      overwrite: yes

    ## Output files to utorrent
    # /DIRECTORY takes to arguments:
    # 1. Save path (now set as %(path)s
    # 2. Torrent file path ( set as %(output)s )
    # Detailed description: http://forum.utorrent.com/viewtopic.php?id=53988&p=1

    exec:
      on_output:
        for_accepted: C:\Progam Files\uTorrent.exe /DIRECTORY "%(path)s" "%(output)s"

  tv:
    rss: http://some.other.tracker.com

    #  Get favourite series from thetvdb.com
    #  Again path variable here is used later
    import_series:
      from: 
        thetvdb_favorites:
          account_id: <my_account_id>
      settings:
        quality: 720p+
        path: C:\Series\%(series_name)s\Season %(series_season)d\
      
    download: 
      path: C:\torrents\
      overwrite: yes

    exec:
      on_output:
        for_accepted: C:\Users\Otto\.flexget\uTorrent.exe /DIRECTORY "%(path)s" "%(output)s"
    
}}}

This should be fine for flexget. Check your configuration with flexget --check.

== Windows 7 and Scheduled tasks  ==

