After reading other users config and Flexget code, I have write my own config and prepare some PR to search movies in Spanish webs.

I have split my config in several files and include in the main config

== Main config ==


{{{
email:
  from: MY_USER@gmail.com
  to: MY_USER@gmail.com
  smtp_host: smtp.gmail.com
  smtp_port: 587
  smtp_username: MY_USER
  smtp_password: MY_PASS
  smtp_tls: yes

tasks:
  mis_series:
    include: 
      - include/series_divxatope.yml
      - include/transmission.yml
      - include/pushover.yml
#      - include/pushbullet.yml
  animeindexfs:
    include:
      - include/animes_fs_animeindex.yml
      - include/transmission.yml
      - include/pushover.yml
#      - include/pushbullet.yml
  nyaafs:
    include:
      - include/animes_fs_nyaa.yml
      - include/transmission.yml
      - include/pushover.yml
#      - include/pushbullet.yml
  minglongfs:
    include:
      - include/animes_fs_minglong.yml
      - include/transmission.yml
      - include/pushover.yml
#      - include/pushbullet.yml
  nyaaevermore:
    include:
      - include/animes_evermore_nyaa.yml
      - include/transmission.yml
      - include/pushover.yml
#      - include/pushbullet.yml
#EOF      

}}}

== Transmission ==


{{{
transmission:
  host: localhost
  port: 9091
  username: USER
  password: PASS
}}}

== PushBullet ==

{{{
pushbullet:
  apikey: API_KEY
}}}

== PushOver ==

{{{
pushover:
  userkey: USER_KEY
  apikey:  API_KEY
  sound: gamelan
}}}

== DivXATope ==


{{{
rss:
  url: http://divxatope.com/feeds.xml
series:
  settings:
    normales:
      ep_regexp:                           
        - Cap.(\d+)(\d\d)                      
      quality: hdtv <720p                  
      path: /volume1/series/{{series_name}}
  normales:
    - Arrow
    - Better Call Saul
    - Community
    - Defiance
    - Falling Skies
    - Futurama
    - Juego de Tronos
    - La Cupula
    - Les Revenants
    - Los 100
    - Padre de Familia
    - Powers:
    - Resurrection
    - Sobrenatural
    - Star Wars Rebels
    - The Big Bang Theory
    - The Walking Dead
    - The Last Ship
    - The Strain
    - True Blood
    - True Detective
    - Ultimo Aviso
    - Vikingos
regexp:
  reject:
    - V.O.:
        from: title
}}}

== '''Working with PR from malkavi github repo, waiting merge''' ==
[https://github.com/Flexget/Flexget/pull/508 PR508]

== Search movies ==

If you remove divxatope from discover, the config will be compatible with the merged version of Flexget.
With the PR you can use elitetorrent at the same way as divxatope to search movies.

{{{
tasks:
  watchlist:
    interval: 2 hours
    imdb_list:
      user_id: USER_ID
      list: watchlist
    accept_all: yes
    seen: local  # We don't want accepted movies on this feed to affect actual download feed
    movie_queue: add              # you could also use `remove` if you wanted to remove the item from your queue
    include: include/pushover.yml
  bajar_pelis:
    priority: 10
    discover:
      what:
        - emit_movie_queue: yes
      from:
        - divxatope:
            category: all
        - kat:
            category: movies
            verified: no
      interval: 1 hours
    torrent_alive: 2 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
    include:
      - include/transmission.yml
      - include/pushover.yml
    movie_queue: accept
    regexp:
      reject:
        - sub[s][\s\._]: {from: title}  # Bloquea todos los torrent que contengan la palabra sub(s) (subtitulos=
        - '[Ll]atino'
        - '[Ss]creener'
      reject_excluding:
        - '[sS]pa|[Cc]astellano'
        - '[Rr]ip'
}}}

== NewPCT1 ==
{{{
rss:
  url: http://www.newpct1.com/feed
  link: link
series:
  settings:
    normales:
      quality: hdtv <720p
      ep_regexp:
        - Cap.(\d+)(\d\d)
  normales:
    - Arrow
    - Juego de Tronos
    - Vikingos
    - Powers
regexp:
  reject:
    - V.O.:
        from: title
download:
  path: /home/osmc/torrents/
}}}

== NewPCT ==

{{{
rss:
  url: http://www.newpct.com/feed/
  link: link
series:
  settings:
    normales:
      quality: hdtv <720p
      ep_regexp:
        - Cap.(\d+)(\d\d)
  normales:
    - Arrow
    - Juego de Tronos
    - Vikingos
    - Powers
regexp:
  reject:
    - V.O.:
        from: title
download: /home/osmc/torrents/
}}}

== EliteTorrent ==

{{{
rss:
  url: http://www.elitetorrent.net/rss.php
series:
  settings:
    normales:
      ep_regexp:                           
        - Cap.(\d+)(\d\d)                      
  normales:
    - Arrow
    - Juego de Tronos
    - Vikingos
    - Powers:
regexp:
  reject:
    - V.O.:
        from: title
download: torrents/
}}}