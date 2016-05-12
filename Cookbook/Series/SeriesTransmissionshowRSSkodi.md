WIP

{{{
tasks:
  # downloading task and remove finished torrents
  # called via cron every 30 minutes. 
  download-showrss:
    rss:
      url: http://showrss.info/user/MYID.rss?magnets=true&namespaces=true&name=clean&quality=null&re=null
    all_series: yes
    transmission: yes
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
    regexp:
      reject:
        - sample
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