This configuration is to be used with the a website like [http://showrss.karmorra.info/ showRSS] where you choose which series you want to watch and the Transmission torrent client.

Let's say a new series you fancy comes out and you want to add it to your download list, instead of opening your configuration file and add it manually (while being prone to all sorts of syntax errors) your go to your showRSS account and add it there, this configuration will fetch all the series it finds from your personal feed at showRSS, download them and organise them with the episode name inside the series folder.

Of course this works will other feeds as well, but the sake of demonstration showRSS is used.  The second example handles a couple gotchas with samples and another way to make sure the sorting tasks does not reject files


{{{
tasks:
  # downloading task
  download-rss:
    rss: http://showrss.karmorra.info/rss.php?user_id=MYUSERACCOUNTNUMBER
    # fetch all the feed series
    all_series: yes
    # use transmission to download the torrents
    transmission:
      host: localhost
      port: 9091
      username: username
      password: password
  # sorting task
  sort-files:
    find:
      # directory with the files to be sorted
      path: /home/solenoid/Downloads/
      # fetch all avi, mkv and mp4 files, skips the .part files (unfinished torrents)
      regexp: '.*\.(avi|mkv|mp4)$'
    accept_all: yes
    seen: local
    # this is needed for the episode names
    thetvdb_lookup: yes
    all_series:
      # for some reason all_series rejects all episodes here, even with seen: local, so parse_only must be added
      parse_only: yes
    # TVDB doesn't recognise "Adventure Time with Finn and Jake" so you must add such exceptions here manually
    series:
      - Adventure Time
    move:
      # this is where the series will be put
      to: /home/solenoid/TV/{{ tvdb_series_name }}
      # save the file as "Series Name - SxxEyy - Episode Name.ext"
      filename: '{{ tvdb_series_name }} - {{ series_id }} - {{ tvdb_ep_name }}{{ location | pathext }}'
}}}

For the complete configuration with Transmission refer to [wiki:Series/SeriesPresetMultipleRSStoTransmission Transmission setup] and use this configuration in ''~/.flexget/config.yml'' file.

== Modified Previous Setup with Kodi Library updates ==

The example below is modified from above to add a few other details.  Ignore samples, cleaning up transmission and using series groups to apply '''parse_only''' because '''accept_all''' did not work for some odd reasion (Currently on flexget 2.0.15)

{{{
tasks:
  # downloading task and remove finished torrents
  # called via cron every 30 minutes.
  # 0,30 * * * * /usr/local/bin/flexget -l /tmp/flexget.log execute --tasks=download-showrss 
  download-showrss:
    rss:
      url: http://showrss.info/user/MYID.rss?magnets=true&namespaces=true&name=clean&quality=null&re=null
    all_series: yes
    transmission: yes
    # you can't delete from transmission immediately anymore, you have to wait until your own transmission seed limits allow
    clean_transmission:
      host: localhost
      port: 9091
      delete_files: yes
      transmission_seed_limits: yes
  # sorting task called on torrent done
  sort-shows:
    filesystem:
      path: /home/htpc/torrent/complete/
      regexp: '.*\.(avi|mkv|mp4)$'
      recursive: yes
    accept_all: yes
    # ignore sample videos that will otherwise cause errors
    regexp:
      reject:
        - sample
    # the only way to apply parse_only to every series is to use series groups.  all_series didn't work for me
    series:
      settings:
        group 1:
          parse_only: yes
      group 1: 
        - Scandal (2012):
            alternate_name: Scandal US
        - Once Upon a Time (2011):
            alternate_name: Once Upon a Time
        - House of Cards (US):
            alternate_name: House of Cards 2013
        - Last Man Standing (2011):
            alternate_name: Last Man Standing US
        - South Park
        - Modern Family
        - The Middle
        - Game of Thrones
        - Homeland
        - Orange Is the New Black
        - The Fall
        - Better Call Saul
        - Luther
        - Silicon Valley
        - Community
        - True Detective
        - Ballers
        - Narcos
        - The X Files
        - Making a Murderer
        - American Crime Story
    thetvdb_lookup: yes
    # using copy instead of move to allow seeding and clean_transmission to remove when done
    copy:
      to: /home/htpc/Videos/TV Shows/{{ tvdb_series_name }}/
      filename: '{{ tvdb_series_name }}.{{ tvdb_ep_id }}'
    kodi_library:
      action: scan
      category: video
      url: http://localhost
      username: kodi
      password: secret
      port: 8080
}}}


== Alternative simple setup ==


{{{
tasks:
  task-a:
    rss: http://showrss.karmorra.info/rss.php?user_id=USERID&hd=2&proper=0
    all_series: yes
    transmission:
      host: localhost
      port: 9091
      username: USERNAME
      password: PASSWORD
      path: /home/xbian/TV/{{series_name}}/Season {{series_season}}
      addpaused: no
}}}