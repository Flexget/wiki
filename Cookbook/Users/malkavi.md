## Download Movies/Series from Spanish webs
After reading other users config and Flexget code, I have write my own config and prepare some PR to search movies in Spanish webs.

I have split my config in several files and include in the main config.
You need to use secretfile.yml with your users/passwords

## Main config

```
secrets: secretfile.yml
templates:
  torrent_server:
    transmission:
      host: localhost
      port: 9091
      username: '{{ secrets.transmission.usr }}'
      password: '{{ secrets.transmission.pwd }}'
  push_notify:
    pushover:
      userkey: '{{ secrets.pushover.usr }}'
      apikey: '{{ secrets.pushover.api }}'
      sound: gamelan
  push_notify2:
    pushbullet:
      apikey: '{{ secrets.pushbullet.key }}'
email:
  from: '{{ secrets.email.from }}'
  to: '{{ secrets.email.to }}'
  smtp_host: smtp.gmail.com
  smtp_port: 587
  smtp_username: '{{ secrets.email.smtp_username }}'
  smtp_password: '{{ secrets.email.smtp_password }}'
  smtp_tls: yes

tasks:
  mis_series:
    template:
      - torrent_server
      - push_notify
    include: 
      - series_divxatope.yml
  animeindexfs:
    template:
      - torrent_server
      - push_notify
    include:
      - animes_fs_animeindex.yml
  nyaafs:
    template:
      - torrent_server
      - push_notify
    include:
      - animes_fs_nyaa.yml
  minglongfs:
    template:
      - torrent_server
      - push_notify
    include:
      - animes_fs_minglong.yml
  nyaaevermore:
    template:
      - torrent_server
      - push_notify
    include:
      - animes_evermore_nyaa.yml
#EOF         

```

## AniRena EverMore
```
rss: 
  url: http://www.anirena.com/rss.php?s=[evermore](/evermore)
  link: link
series:
  settings:
    anime:
      path: /volume1/animes/{{series_name}}
  anime:
    - Aldnoah Zero
    - Captain Earth
    - Knights of Sidonia S2
regexp:
  reject_excluding:
    - '\[EvermorE\](/EvermorE\)'
  reject:
    - mkv
```

## AnimeIndex FallenSubs
```
rss: http://tracker.anime-index.org/rss.php
series:
  settings:
    anime_fs:
      path: /volume1/animes/{{series_name}}
      from_group:
        - FS
  anime_fs:
    - Absolute Duo
    - Akame ga Kill!
    - Akuma no Riddle
    - Amagi Brilliant Park
    - Chuunibyou demo
    - Date A Live II
    - Death Parade
    - Dungeon ni Deai
    - Fairy Tail
    - Glasslip
    - Gokukoku
    - Grisaia no Meikyuu
    - Grisaia no Kajitsu
    - Grisaia no Rakuen
    - Hibike! Euphonium
    - Highschool DxD
    - Highschool DxD BorN:
        path: /volume1/animes/Highschool DxD
    - Houkago no Pleiades
    - ISUCA
    - Juuou Mujin no Fafnir
    - Kantai Collection
    - Madan no Ou to Vanadis
    - Mahou Sensou
    - Mahouka Koukou
    - Nisekoi
    - Plastic Memories
    - Rail Wars
    - Saenai Heroine no Sodatekata
    - Seiken Tsukai no World Break
    - Seikoku no Dragonar
    - Seirei Tsukai no Blade Dance
    - Sora no Method
    - Strike the Blood
    - Sword Art Online II:
        path: /volume1/animes/SAO
    - Trinity Seven
regexp:
  reject:
    - Vol
  from: title
manipulate:
  - title:
      extract: .*\[TORRENT\](/TORRENT\) (.*)
```

## DivXATope

```
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
    - Extant
    - Falling Skies
    - Futurama
    - Juego de Tronos
    - La Cupula
    - Les Revenants
    - Los 100
    - Padre de Familia
    - Powers
    - Resurrection
    - Sobrenatural
    - Star Wars Rebels
    - The Big Bang Theory
    - The Flash
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
```

## **Working with PR from malkavi github repo, waiting merge**
[PR516](https://github.com/Flexget/Flexget/pull/516)

## Search movies
If you remove divxatope from discover, the config will be compatible with the merged version of Flexget.
With the PR you can use elitetorrent at the same way as divxatope to search movies.

```
secrets: secretfile.yml
templates:
  torrent_server:
    transmission:
      host: localhost
      port: 9091
      username: '{{ secrets.transmission.usr }}'
      password: '{{ secrets.transmission.pwd }}'
  push_notify:
    pushover:
      userkey: '{{ secrets.pushover.usr }}'
      apikey: '{{ secrets.pushover.api }}'
      sound: gamelan
  push_notify2:
    pushbullet:
      apikey: '{{ secrets.pushbullet.key }}'
email:
  from: '{{ secrets.email.from }}'
  to: '{{ secrets.email.to }}'
  smtp_host: smtp.gmail.com
  smtp_port: 587
  smtp_username: '{{ secrets.email.smtp_username }}'
  smtp_password: '{{ secrets.email.smtp_password }}'
  smtp_tls: yes
  
tasks:
  watchlist:
#    priority: 1
    interval: 2 hours
    imdb_list:
      user_id: '{{ secrets.imdb.user_id }}'
      list: watchlist
    accept_all: yes
    seen: local  # We don't want accepted movies on this feed to affect actual download feed
    movie_queue: add              # you could also use `remove` if you wanted to remove the item from your queue
    template:
      - push_notify
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
#        - piratebay:
#            category: video
#            sort_by: default
#        - torrentz: verified
      interval: 1 hours
#      type: movies
    torrent_alive: 2 # Will reject results with less than 10 seeds
    quality: dvdrip+ # Make sure no screeners or cams are downloaded
#    download: torrents/
    template:
      - torrent_server
      - push_notify
    movie_queue: accept
    regexp:
      reject:
        - sub[s](/s)[\s\._](/\s\._): {from: title}  # Bloquea todos los torrent que contengan la palabra sub(s) (subtitulos=
        - '[Ll](/Ll)atino'
        - '[Ss](/Ss)creener'
      reject_excluding:
        - '[sS](/sS)pa|[Cc](/Cc)astellano'
        - '[Rr](/Rr)ip'
```

## NewPCT1
```
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
```

## NewPCT
```
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
```

## EliteTorrent
```
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
```